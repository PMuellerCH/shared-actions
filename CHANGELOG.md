# Changelog

## [1.1.3](https://github.com/PMuellerCH/shared-actions/compare/v1.1.2...v1.1.3) (2026-11-24)


### Bug Fixes

* pass github.token to molecule test as GITHUB_TOKEN ([#17](https://github.com/PMuellerCH/shared-actions/issues/17)) ([4ac3deb](https://github.com/PMuellerCH/shared-actions/commit/4ac3debf8c1b024b181c7f01ff22038c81470399)), closes [#16](https://github.com/PMuellerCH/shared-actions/issues/16)


### Miscellaneous

* **deps:** update bridgecrewio/checkov-action action to v12.3146.0 ([#15](https://github.com/PMuellerCH/shared-actions/issues/15)) ([142f08f](https://github.com/PMuellerCH/shared-actions/commit/142f08fe3ba5bb539f956e04acce46d6914f8268))
* **deps:** update davidanson/markdownlint-cli2-action action to v25.1.0 ([#14](https://github.com/PMuellerCH/shared-actions/issues/14)) ([f1f6bd0](https://github.com/PMuellerCH/shared-actions/commit/f1f6bd0ca02a8bd8b92fd5e67758075e67b0772d))


### Documentation

* document path-filtered molecule on every PR ([#13](https://github.com/PMuellerCH/shared-actions/issues/13)) ([1164727](https://github.com/PMuellerCH/shared-actions/commit/11647270e2f07687b33f7f83ec169f9a001a40d4)), closes [#12](https://github.com/PMuellerCH/shared-actions/issues/12)

## [1.1.2](https://github.com/PMuellerCH/shared-actions/compare/v1.1.1...v1.1.2) (2026-11-19)


### Miscellaneous

* **deps:** update ansible/ansible-lint action to v26.11.0 ([#9](https://github.com/PMuellerCH/shared-actions/issues/9)) ([a538342](https://github.com/PMuellerCH/shared-actions/commit/a53834297717715c09ce0f3798f808e6118c7a7b))
* **deps:** update bridgecrewio/checkov-action action to v12.3122.0 ([#6](https://github.com/PMuellerCH/shared-actions/issues/6)) ([6530621](https://github.com/PMuellerCH/shared-actions/commit/65306210df2a120dbbaefa2c410ad64a4a65329d))
* **deps:** update bridgecrewio/checkov-action action to v12.3142.0 ([#8](https://github.com/PMuellerCH/shared-actions/issues/8)) ([434ef99](https://github.com/PMuellerCH/shared-actions/commit/434ef99d6be7c25f49e8df3af7cbcabd82288e18))
* **deps:** update davidanson/markdownlint-cli2-action action to v25 ([#11](https://github.com/PMuellerCH/shared-actions/issues/11)) ([c680aa8](https://github.com/PMuellerCH/shared-actions/commit/c680aa86c9945a8c9893409645805543a35f28ce))
* **deps:** update dependency python to 3.15 ([#10](https://github.com/PMuellerCH/shared-actions/issues/10)) ([49f2fe2](https://github.com/PMuellerCH/shared-actions/commit/49f2fe22837148c4831416fb004792e52218d535))

## [1.1.1](https://github.com/PMuellerCH/shared-actions/compare/v1.1.0...v1.1.1) (2026-08-20)


### Miscellaneous

* **deps:** update bridgecrewio/checkov-action action to v12.3119.0 ([#1](https://github.com/PMuellerCH/shared-actions/issues/1)) ([7e0bff1](https://github.com/PMuellerCH/shared-actions/commit/7e0bff1cdeb5b6d5391dac585d5c5deaf8de5e7d))
* **deps:** update dependency python to 3.14 ([#2](https://github.com/PMuellerCH/shared-actions/issues/2)) ([e6dd05c](https://github.com/PMuellerCH/shared-actions/commit/e6dd05c48db19d6245b8bd50eaeacd8b2ee74a7d))

## [1.1.0](https://github.com/PMuellerCH/shared-actions/compare/v1.0.0...v1.1.0) (2026-08-20)


### Features

* add install-self-collection input to ansible_lint.yml ([7641796](https://github.com/PMuellerCH/shared-actions/commit/7641796b8a8dffe33b1a7c897ca6c4e6610c449d))
* add release-please automation ([f7da395](https://github.com/PMuellerCH/shared-actions/commit/f7da395a113cc087ac43382db19a0becc6f6aa2d))
* initial reusable workflows for Ansible collection CI ([370895d](https://github.com/PMuellerCH/shared-actions/commit/370895d1ab2920a88c42ddb88e9da87b4e07cef7))


### Bug Fixes

* exclude .ansible/ from markdownlint standard-files glob ([f4524b2](https://github.com/PMuellerCH/shared-actions/commit/f4524b23365ac5d9ed2fc98491daee68cbc08006))
* hardcode tool versions in ansible-lint composite action ([cc141da](https://github.com/PMuellerCH/shared-actions/commit/cc141da67dc265eb15b80df0226e914557c27cd3))
* inline third-party lint actions directly in ansible_lint.yml ([e40e753](https://github.com/PMuellerCH/shared-actions/commit/e40e7530977baa7fc39cddfbfef735e4234bb44f))
