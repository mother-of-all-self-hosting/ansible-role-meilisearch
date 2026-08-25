<!--
SPDX-FileCopyrightText: 2023 Slavi Pantaleev
SPDX-FileCopyrightText: 2025, 2026 Suguru Hirahara

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Meilisearch Ansible role

This is an [Ansible](https://www.ansible.com/) role which installs [Meilisearch](https://www.meilisearch.com) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

This role *implicitly* depends on:

- [`com.devture.ansible.role.playbook_help`](https://github.com/devture/com.devture.ansible.role.playbook_help)
- [`com.devture.ansible.role.systemd_docker_base`](https://github.com/devture/com.devture.ansible.role.systemd_docker_base)

Check [`defaults/main.yml`](defaults/main.yml) for the full list of supported options. Refer to [this page](docs/configuring-meilisearch.md) for details about setting up the service with this role.

💡 For an Ansible playbook which integrates this role and makes it easier to use, see the [Mother-of-All-Self-Hosting Ansible playbook](https://github.com/mother-of-all-self-hosting/mash-playbook).

>[!NOTE]
> Please note that `v1.28.0` has introduced a separation into "pro" and "peasant" editions:
>
> "This release introduces improvements to language support and separates the community and enterprise binary editions. We now offer binaries [under the BUSL-1.1 license](https://redirect.github.com/meilisearch/meilisearch/blob/main/LICENSE-EE), identified by the "enterprise" term in their names, in addition to our MIT-licensed binaries, which retain their original names. Docker images for the enterprise edition are available in the [`getmeili/meilisearch-enterprise`](https://hub.docker.com/r/getmeili/meilisearch-enterprise/tags) repository."
>
> See: <https://github.com/mother-of-all-self-hosting/ansible-role-meilisearch/pull/8>

## Development

### pre-commit

You can optionally install a Git pre-commit hook (via [mise](https://mise.jdx.dev/) + [prek](https://prek.j178.dev/)) that runs formatting and linting checks before each commit. See [`.pre-commit-config.yaml`](./.pre-commit-config.yaml) for which hooks are to be executed.

To install the hook, run the [`just`](https://github.com/casey/just) command below:

```sh
just prek-install-git-pre-commit-hook
```

### Molecule

This role supports [Molecule](https://docs.ansible.com/projects/molecule/), an Ansible testing framework designed for developing and testing Ansible collections, playbooks, and roles.

Refer to [this page](./molecule/README.md) for details about how to utilize it.
