[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx__app__protect-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx_app_protect)
[![Build Status](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect.svg?branch=main)](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect)
[![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# 👾 *Help make the NGINX App Protect Ansible role better by participating in our [survey](https://forms.office.com/Pages/ResponsePage.aspx?id=L_093Ttq0UCb4L-DJ9gcUKLQ7uTJaE1PitM_37KR881UM0NCWkY5UlE5MUYyWU1aTUcxV0NRUllJSC4u)!* 👾

# NGINX App Protect Ansible Role <img src="images/nap-logo.png" width="30">

This role installs and configures NGINX App Protect (WAF) for NGINX Plus on your target host.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

## Requirements

### Ansible

*   This role is developed and tested with [maintained](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html) versions of Ansible core (above `2.11`) and Ansible (above `2.9.10`).
*   When using Ansible base, you will also need to install the following collections:
    ```yaml
    ---
    collections:
      - name: community.general
        version: 3.1.0
      - name: ansible.posix
        version: 1.2.0
    ```
    **Note:** You can alternatively install the Ansible community distribution (what is known as the "old" Ansible) if you don't want to manage individual collections.
*   Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#upgrading-ansible-from-version-2-9-and-older-to-version-2-10-or-later).

### Jinja2

*   This role uses Jinja2 templates. Ansible base installs Jinja2 by default, but depending on your install and/or upgrade path, you might be running an outdated version of Jinja2. The minimum version of Jinja2 required for the role to properly function is `2.11`.
*   Instructions on how to install Jinja2 can be found in the [Jinja2 website](https://jinja.palletsprojects.com/en/2.11.x/intro/#installation).

### Molecule

*   Molecule is used to test the various functionalities of the role. The recommended version of Molecule to test this role is `3.3`.
*   Instructions on how to install Molecule can be found in the [Molecule website](https://molecule.readthedocs.io/en/latest/installation.html).
*   To run the Molecule tests, you must first add your NGINX repository certificate and key to the local environment. Run the following commands to export these files as base64-encoded variables and execute the Molecule tests:
    ``` bash
    export NGINX_CRT=$( cat <path to your certificate file> | base64 )
    export NGINX_KEY=$( cat <path to your key file> | base64 )
    molecule test
    ```
    You can alternatively copy your NGINX license to the role's [`files/license`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/files/license/) folder.

## Installation

### Ansible Galaxy

Use `ansible-galaxy install nginxinc.nginx_app_protect` to install the latest stable release of the role on your system.

### Git

Use `git clone https://github.com/nginxinc/ansible-role-nginx-app-protect.git` to pull the latest edge commit of the role from GitHub.

## Platforms

The NGINX App Protect Ansible role supports all platforms supported by [NGINX Plus](https://www.nginx.com/products/technical-specs/) that intersect with the following list:

```yaml
CentOS:
  - 7.4+
RHEL:
  - 7.4+
Debian:
  - 9
Ubuntu:
  - 18.04
  - 20.04
```

**Note:** Due to a packaging limitation in NGINX App Protect on Alpine, it may be required to explicitly install NGINX Plus on the instance **before** using the NGINX App Protect role if a hotfix version of NGINX Plus has been published. It is recommended to use the [NGINX Core](https://galaxy.ansible.com/nginxinc/nginx_core) Ansible role for this purpose.

## Role Variables

This role has multiple variables. The descriptions and defaults for all these variables can be found in the **[`defaults/`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/defaults/)** folder in the following files:

|Name|Description|
|----|-----------|
|**[`main.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/defaults/main.yml)**:|NGINX App Protect installation and configuration variables|

Similarly, descriptions and defaults for preset variables can be found in the **`vars/`** folder in the following files:

|Name|Description|
|----|-----------|
|**[`main.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/vars/main.yml)**|List of supported NGINX App Protect platforms|

## Dependencies

*   If NGINX Plus is *not* already installed on the system, this role will install the version of NGINX Plus that is dependent on the version of NGINX App Protect that is being installed.

## Example Playbook

A working functional playbook example can be found in the **`molecule/default/`** folder in the following file:

|Name|Description|
|----|-----------|
|**[`molecule/default/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/molecule/default/converge.yml)**|Install and configure NGINX App Protect|

## Other NGINX Ansible Collections and Roles

You can find the Ansible NGINX Core collection of roles to install and configure NGINX Open Source, NGINX Plus, and NGINX App Protect [here](https://github.com/nginxinc/ansible-collection-nginx).

You can find the Ansible NGINX role to install NGINX [here](https://github.com/nginxinc/ansible-role-nginx).

You can find the Ansible NGINX configuration role to configure NGINX [here](https://github.com/nginxinc/ansible-role-nginx-config).

You can find the Ansible NGINX Controller collection of roles to install and configure NGINX Controller [here](https://github.com/nginxinc/ansible-collection-nginx_controller).

You can find the Ansible NGINX Unit role to install NGINX Unit [here](https://github.com/nginxinc/ansible-role-nginx-unit).

## License

[Apache License, Version 2.0](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/LICENSE)

## Author Information

[Daniel Edgar](https://github.com/aknot242)

[Alessandro Fael Garcia](https://github.com/alessfg)

&copy; [F5 Networks, Inc.](https://www.f5.com/) 2020 - 2021
