# PMuellerCH/shared-actions

Reusable GitHub Actions workflows and composite actions for PMuellerCH's Ansible collections
(`ansible-collection-workstation` and future ones) and implementation/playbook repos
(`computer-setup`).

Mirrors the design of swisstopo's `infra-github-shared-actions` (not reusable outside the
swisstopo org, hence this separate repo): reusable workflows own orchestration, tool config
stays in the calling repo, and composite actions under `.github/actions/` are internal
building blocks — call the workflows in `.github/workflows/`, not the actions directly.

## Versioning

Consumers **must** pin to the floating major-version tag (`@v1`, not `@main`), the same
convention official actions like `actions/checkout@v4` use. Releases are cut by
[release-please](https://github.com/googleapis/release-please) from Conventional Commits on
every push to `main`, producing real semver tags (`v1.2.3`); a second job then force-moves the
`v1` tag to point at the newest release in that major line. Consumers pinned to `@v1`
therefore pick up every patch/minor release **silently, with no PR of their own** — this is
deliberate: it's what makes the floating-tag convention useful (no per-consumer churn for
routine fixes), same as how `actions/checkout@v4` updates work.

This is a real tradeoff, not a free lunch: it means a consumer never explicitly reviews a
routine `v1.x.y` bump before it takes effect on their next CI run — the review gate for
changes here is this repo's own PR process, not each consumer's. A **major** bump (`v2`) is
never silent: it requires every consumer to deliberately change their own `@v1` pin, so a
breaking change can never propagate without an explicit action on the consuming side.

Consumers can still audit or pin to an exact `v1.2.3` tag directly if they ever need to bypass
the floating tag for a specific reason (e.g. bisecting a regression).

## Reusable workflows

### `ansible_lint.yml`

Runs yamllint, [`ansible/ansible-lint`](https://github.com/ansible/ansible-lint) (official
action), [`DavidAnson/markdownlint-cli2-action`](https://github.com/DavidAnson/markdownlint-cli2-action)
(official action, two-pass — standard files + a relaxed pass for `CHANGELOG.md`), and
[`bridgecrewio/checkov-action`](https://github.com/bridgecrewio/checkov-action) (official
action). All three third-party tools use their own actively-maintained official actions
rather than reimplementing pip/npm install-and-run steps — researched before building this,
see git history for what was checked and rejected (e.g. no well-maintained molecule action
exists, so that one *is* built from scratch).

```yaml
jobs:
  lint:
    uses: PMuellerCH/shared-actions/.github/workflows/ansible_lint.yml@v1
```

All inputs are optional. Set `checkov-framework: 'all'` for implementation repos with
mixed content (not just Ansible). Set `ansible-requirements-file: requirements.yml` if your
repo has Galaxy collection dependencies ansible-lint needs installed to resolve module
references (e.g. `community.general.flatpak`).

### `ansible_molecule.yml`

Runs `molecule test` for every role under `roles-base-path` with a `roles/<name>/molecule/default/`
scenario (auto-discovered — no hardcoded list to forget to update), one per matrix job.

```yaml
jobs:
  molecule:
    if: >-
      startsWith(github.head_ref, 'release-please--') ||
      startsWith(github.head_ref, 'renovate/') ||
      github.event_name == 'workflow_dispatch'
    uses: PMuellerCH/shared-actions/.github/workflows/ansible_molecule.yml@v1
```

**The `if:` condition is the caller's responsibility, not this workflow's** — controls when
molecule runs (e.g. not on every ordinary PR, since a full molecule run is too slow to gate
routine iteration). **Include the `renovate/` branch prefix if you intend to gate Renovate
automerge on this check** — omitting it means molecule silently never runs on Renovate PRs,
making "tests pass" a vacuous automerge gate.

Set `install-self-collection: 'false'` for implementation/playbook repos (the default `'true'`
assumes the repo is itself a Galaxy collection that should `ansible-galaxy collection install .`
before testing).

See [`example/ansible_example_workflow.yml`](example/ansible_example_workflow.yml) for full
collection-repo and implementation-repo worked examples.

## Composite actions (internal only — do not call directly)

- `ansible-setup` — Python environment + pip install from a requirements file. Used by both
  reusable workflows above for their respective tool needs.
- `ansible-molecule-role` — installs Galaxy dependencies (cached) and runs `molecule test`
  for a single role. Called once per matrix item by `ansible_molecule.yml`.

These exist to keep the reusable workflows readable; their input/output contracts are not
considered stable for direct external use and may change without a major version bump.

**Do not wrap a third-party action in one of these composite actions if that action
inspects its own ref/version at runtime** (e.g. to fetch a matching requirements lockfile,
as `ansible/ansible-lint`'s own `action.yml` does). GitHub Actions has a long-standing
runner bug where `GITHUB_ACTION_REF`/`github.action_ref` resolves to the *outer* composite
action's ref instead of the nested action's own pinned ref
([actions/runner#2473](https://github.com/actions/runner/issues/2473),
[actions/runner#2525](https://github.com/actions/runner/issues/2525)). `ansible_lint.yml`
calls `ansible/ansible-lint`, `DavidAnson/markdownlint-cli2-action`, and
`bridgecrewio/checkov-action` directly as job steps for this reason, not through a
composite action.

## Development

This repo has no roles or Ansible content of its own to lint/test — it's pure GitHub Actions
YAML. Validate changes by pointing a consumer repo's workflow at a branch or commit SHA
before tagging a release.
