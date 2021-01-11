[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx__app__protect-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx_app_protect)
[![Build Status](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect.svg?branch=main)](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect)
[![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# 👾 *Help make the NGINX App Protect Ansible role better by participating in our [survey](https://forms.office.com/Pages/ResponsePage.aspx?id=L_093Ttq0UCb4L-DJ9gcUKLQ7uTJaE1PitM_37KR881UM0NCWkY5UlE5MUYyWU1aTUcxV0NRUllJSC4u)!* 👾

# NGINX App Protect Ansible Role <img src="images/nap-logo.png" width="30">

This role installs and configures NGINX App Protect (WAF) for NGINX Plus on your target host.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

## Requirements

### Ansible

*   This role is developed and tested with [maintained](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#release-status) versions of Ansible. Backwards compatibility is not guaranteed.
*   Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

### Molecule

*   Molecule `3.x` is used to test the various functionalities of the role.
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
```

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

*   Since this role uses the [package_facts](https://docs.ansible.com/ansible/latest/modules/package_facts_module.html) module, on debian-based systems the `python-apt` package must be installed on targeted hosts.

*   If NGINX Plus is *not* already installed on the system, this role will install the version of NGINX Plus that is dependent on the version of NGINX App Protect set with the `nginx_app_protect_version` variable. If none is specified, the latest version of NGINX Plus and NGINX App Protect will be installed.

*   When using the `nginx_app_protect_version` variable, a specific version of NGINX Plus must already be installed on the target system.

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
