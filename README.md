<!--
SPDX-FileCopyrightText: 2023 Slavi Pantaleev
SPDX-FileCopyrightText: 2025 Suguru Hirahara

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Meilisearch Ansible role

This is an [Ansible](https://www.ansible.com/) role which installs [Meilisearch](https://www.meilisearch.com) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

This role *implicitly* depends on:

- [`com.devture.ansible.role.playbook_help`](https://github.com/devture/com.devture.ansible.role.playbook_help)
- [`com.devture.ansible.role.systemd_docker_base`](https://github.com/devture/com.devture.ansible.role.systemd_docker_base)

Check [defaults/main.yml](defaults/main.yml) for the full list of supported options.

💡 See this [document](docs/configuring-meilisearch.md) for details about setting up the service with this role.

>[!NOTE]
> Please note that the `v1.28.0` has introduced the "pro" and "peasant" editions separation:
>
> "This release introduces improvements to language support and separates the community and enterprise binary editions. We now offer binaries [under the BUSL-1.1 license](https://redirect.github.com/meilisearch/meilisearch/blob/main/LICENSE-EE), identified by the "enterprise" term in their names, in addition to our MIT-licensed binaries, which retain their original names. Docker images for the enterprise edition are available in the [`getmeili/meilisearch-enterprise`](https://hub.docker.com/r/getmeili/meilisearch-enterprise/tags) repository."
>
> See: <https://github.com/mother-of-all-self-hosting/ansible-role-meilisearch/pull/8>

## Development

You can optionally install [pre-commit](https://pre-commit.com/) so that simple mistakes are checked and noticed before changes are pushed to a remote branch. See [`.pre-commit-config.yaml`](./.pre-commit-config.yaml) for which hooks are to be executed.

See [this section](https://pre-commit.com/#usage) on the official documentation for usage.
