<img src="images/nap-logo.png" width="60">

NGINX App Protect Ansible Role
==============================

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx_app_protect)
[![Build Status](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect.svg?branch=main)](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect)

This role installs and configures NGINX App Protect (WAF) for NGINX Plus on your target host.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

Requirements
------------

**Ansible**

This role was developed and tested with [maintained](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#release-status) versions of Ansible. Backwards compatibility is not guaranteed.

Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

**Molecule**

Molecule is used to test the various functionalities of the role. Instructions on how to install Molecule can be found in the [Molecule website](https://molecule.readthedocs.io/en/stable/installation.html).

To run the Molecule tests, you must first add your NGINX repository certificate and key to the local environment. Run the following commands to export these files as base64-encoded variables and execute the Molecule tests:

``` bash
export NGINX_CRT=$( cat <path to your certificate file> | base64)
export NGINX_KEY=$( cat <path to your key file> | base64)
molecule test
```

Installation
------------

**Ansible Galaxy**

Use `ansible-galaxy install nginxinc.nginx_app_protect` to install the latest stable release of the role on your system.

**Git**

Use `git clone https://github.com/nginxinc/ansible-role-nginx-app-protect.git` to pull the latest edge commit of the role from GitHub.

Platforms
---------

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

Role Variables
--------------

This role has multiple variables. The descriptions and defaults for all these variables can be found in the **`defaults`** directory in the following files:

-   **[defaults/main.yml](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/defaults/main.yml)**: NGINX App Protect installation and configuration variables

Similarly, descriptions and defaults for preset variables can be found in the **`vars`** directory in the following files:

-   **[vars/main.yml](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/vars/main.yml):** List of supported NGINX App Protect platforms

Dependencies
------------

-   Since this role uses the [package_facts](https://docs.ansible.com/ansible/latest/modules/package_facts_module.html) module, on debian-based systems the `python-apt` package must be installed on targeted hosts.

-   If NGINX Plus is *not* already installed on the system, this role will install the version of NGINX Plus that is dependent on the version of NGINX App Protect set with the `nginx_app_protect_version` variable. If none is specified, the latest version of NGINX Plus and NGINX App Protect will be installed.

-   When using the `nginx_app_protect_version` variable, a specific version of NGINX Plus must already be installed on the target system.

Example Playbook
----------------

A working functional playbook example can be found in the **`molecule/default`** directory in the following file:

-   **[molecule/default/converge.yml](https://github.com/nginxinc/ansible-role-nginx-app_protect/blob/main/molecule/default/converge.yml):** Install and configure NGINX App Protect

Other NGINX Roles
-----------------

You can find an Ansible role to install NGINX [here](https://github.com/nginxinc/ansible-role-nginx)

You can find an Ansible role to configure NGINX [here](https://github.com/nginxinc/ansible-role-nginx-config)

You can find an Ansible collection of roles to help you install and configure NGINX Controller [here](https://github.com/nginxinc/ansible-collection-nginx_controller)

You can find an Ansible role to install NGINX Unit [here](https://github.com/nginxinc/ansible-role-nginx-unit)

License
-------

[Apache License, Version 2.0](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/LICENSE)

Author Information
------------------

[Daniel Edgar](https://github.com/aknot242)

[Alessandro Fael Garcia](https://github.com/alessfg)

&copy; [F5 Networks, Inc.](https://www.f5.com/) 2020
