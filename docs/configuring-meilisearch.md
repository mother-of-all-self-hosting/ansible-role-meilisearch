<!--
SPDX-FileCopyrightText: 2020 - 2024 MDAD project contributors
SPDX-FileCopyrightText: 2020 - 2024 Slavi Pantaleev
SPDX-FileCopyrightText: 2020 Aaron Raimist
SPDX-FileCopyrightText: 2020 Chris van Dijk
SPDX-FileCopyrightText: 2020 Dominik Zajac
SPDX-FileCopyrightText: 2020 Mickaël Cornière
SPDX-FileCopyrightText: 2022 François Darveau
SPDX-FileCopyrightText: 2022 Julian Foad
SPDX-FileCopyrightText: 2022 Warren Bailey
SPDX-FileCopyrightText: 2023 Antonis Christofides
SPDX-FileCopyrightText: 2023 Felix Stupp
SPDX-FileCopyrightText: 2023 Julian-Samuel Gebühr
SPDX-FileCopyrightText: 2023 Pierre 'McFly' Marty
SPDX-FileCopyrightText: 2024 Thomas Miceli
SPDX-FileCopyrightText: 2024 - 2025 Suguru Hirahara

SPDX-License-Identifier: AGPL-3.0-or-later
-->

# Setting up Meilisearch

This is an [Ansible](https://www.ansible.com/) role which installs [Meilisearch](https://www.meilisearch.com) to run as a [Docker](https://www.docker.com/) container wrapped in a systemd service.

Meilisearch is a fast and typo-tolerant fulltext search engine with a RESTful search API.

See the project's [documentation](https://www.meilisearch.com/docs/learn/self_hosted/getting_started_with_self_hosted_meilisearch) to learn what Meilisearch does and why it might be useful to you.

## Adjusting the playbook configuration

To enable Meilisearch with this role, add the following configuration to your `vars.yml` file.

**Note**: the path should be something like `inventory/host_vars/mash.example.com/vars.yml` if you use the [MASH Ansible playbook](https://github.com/mother-of-all-self-hosting/mash-playbook).

```yaml
########################################################################
#                                                                      #
# meilisearch                                                          #
#                                                                      #
########################################################################

meilisearch_enabled: true

########################################################################
#                                                                      #
# /meilisearch                                                         #
#                                                                      #
########################################################################
```

### Set the master key

You also need to specify the instance's master key, a UTF-8 string of at least 16 bytes.

To do so, add the following configuration to your `vars.yml` file. The value can be generated with `pwgen -s 64 1` or in another way.

```yaml
meilisearch_environment_variables_master_key: YOUR_SECRET_KEY_HERE
```

>[!WARNING]
> It is [not recommended](https://www.meilisearch.com/docs/learn/security/basic_security) to use the master key for operations anything but managing other API keys. See [this section](#obtaining-api-keys) below for the instruction to obtain those keys.

### Exposing the instance (optional)

By default, the Meilisearch instance is not exposed externally, as it is mainly intended to be used in the internal network, connected to other services.

To expose it to the internet, add the following configuration to your `vars.yml` file. Make sure to replace `example.com` with your own value.

```yaml
meilisearch_hostname: "example.com"

meilisearch_container_labels_traefik_enabled: true
```

After adjusting the hostname, make sure to adjust your DNS records to point the domain to your server.

**Note**: hosting Meilisearch under a subpath (by configuring the `meilisearch_path_prefix` variable) does not seem to be possible due to Meilisearch's technical limitations.

### Extending the configuration

There are some additional things you may wish to configure about the component.

Take a look at:

- [`defaults/main.yml`](../defaults/main.yml) for some variables that you can customize via your `vars.yml` file. You can override settings (even those that don't have dedicated playbook variables) using the `meilisearch_environment_variables_additional_variables` variable

See [the official documentation](https://www.meilisearch.com/docs/learn/self_hosted/configure_meilisearch_at_launch) for a complete list of Meilisearch's config options that you could put in `meilisearch_environment_variables_additional_variables`.

## Installing

After configuring the playbook, run the installation command of your playbook as below:

```sh
ansible-playbook -i inventory/hosts setup.yml --tags=setup-all,start
```

If you use the MASH playbook, the shortcut commands with the [`just` program](https://github.com/mother-of-all-self-hosting/mash-playbook/blob/main/docs/just.md) are also available: `just install-all` or `just setup-all`

## Usage

After running the command for installation, Meilisearch becomes available internally to other services on the same network. If the service is exposed to the internet, it becomes available at the specified hostname like `https://example.com`.

See [this page](https://www.meilisearch.com/docs/learn/getting_started/what_is_meilisearch) on the documentation about its usage.

### Obtaining API keys

You can run the playbook with the `obtain-api-keys-meilisearch` tag as below to get the API keys:

```sh
ansible-playbook -i inventory/hosts setup.yml --tags=obtain-api-keys-meilisearch
```

## Troubleshooting

### Check the service's logs

You can find the logs in [systemd-journald](https://www.freedesktop.org/software/systemd/man/systemd-journald.service.html) by logging in to the server with SSH and running `journalctl -fu meilisearch` (or how you/your playbook named the service, e.g. `mash-meilisearch`).
