# Anarcho-Tech NYC: Radicale [![Build Status](https://travis-ci.org/AnarchoTechNYC/ansible-role-radicale.svg?branch=master)](https://travis-ci.org/AnarchoTechNYC/ansible-role-radicale)

An [Ansible role](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html) for installing a [Radicale](http://radicale.org/) server. Notably, this role has been tested with [Raspbian](https://www.raspbian.org/) on [Raspberry Pi](https://www.raspberrypi.org/) hardware. This role's purpose is to make it simple to install a CalDAV and CardDAV server.

# Configuring Radicale

To configure your Radicale server instance, use the `radicale_config` dictionary. The keys in this dictionary map nearly one-to-one to the configuration directives described in [Radicale's Configuration documentation page](https://radicale.org/configuration/). Configuration directive groups are their own dictionaries, and directives that can accept more than one value are specified as a list.

Some examples may prove helpful:

1. Simple Radicale server with default for all values:
    ```yaml
    radicale_config:
    ```
1. Simple Radicale server bound to the local host only and listening on the alternative HTTP port:
    ```yaml
    radicale_config:
      server:
        hosts:
          - addr: 127.0.0.1
            port: 8080
    ```

See the comments in the [`defaults/main.yaml`](defaults/main.yaml) file for additional details.

# Adding or removing Radicale user accounts

The `radicale_users` variable is a list containing dictionaries for each user account. Each user account dictionary in the list can have the following keys:

* `name`: The name of the user account. This key is required.
* `password`: The password for this user account. It is recommended to encrypt this value with Ansible Vault. If this is omitted, the `bcrypt_hash` key is required.
* `bcrypt_hash`: Instead of supplying a password, you can supply a bcrypt hash of the password in `passlib` format. If this is omitted, the `password` key is required.
* `state`: Whether the user should exist (`present`) or not (`absent`). This key is optional.
