Ansible NGINX Role
==================

[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx)
[![Build Status](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect.svg?branch=master)](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect)

This role installs and configures NGINX App Protect (WAF) for NGINX Plus, on your target host.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

Requirements
------------

**Ansible**

This role was developed and tested with [maintained](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#release-status) versions of Ansible. Backwards compatibility is not guaranteed.

Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

**Molecule**

Molecule is used to test the various functionalities of the role. Instructions on how to install Molecule can be found in the [Molecule website](https://molecule.readthedocs.io/en/stable/installation.html).

Installation
------------

**Ansible Galaxy**

Use `ansible-galaxy install nginxinc.nginx_app_protect` to install the latest stable release of the role on your system.

**Git**

Use `git clone https://github.com/nginxinc/ansible-role-nginx-app-protect.git` to pull the latest edge commit of the role from GitHub.

Platforms
---------

The NGINX Ansible role supports all platforms supported by [NGINX Plus](https://www.nginx.com/products/technical-specs/):


**NGINX Plus**

```yaml
Alpine:
  versions:
    - 3.8
    - 3.9
    - 3.10
Amazon Linux:
  versions:
    - 2018.03
Amazon Linux 2:
  versions:
    - LTS
CentOS:
  versions:
    - 6.5+
    - 7.4+
    - 8
Debian:
  versions:
    - stretch
    - buster
FreeBSD:
  versions:
    - 11.2+
    - 12
Oracle Linux:
  versions:
    - 6.5+
    - 7.4+
RedHat:
  versions:
    - 6.5+
    - 7.4+
    - 8
SUSE/SLES:
  versions:
    - 12
    - 15
Ubuntu:
  versions:
    - xenial
    - bionic
```

Role Variables
--------------

This role has multiple variables. The descriptions and defaults for all these variables can be found in the directory **`defaults/main`** in the following files:

-   **[defaults/main/main.yml](./defaults/main/main.yml):** NGINX installation variables
-   **[defaults/main/upload.yml](./defaults/main/upload.yml):** NGINX configuration/HTML/SSL upload variables
-   **[defaults/main/linux.yml](./defaults/main/linux.yml):** Linux installation variables
-   **[defaults/main/bsd.yml](./defaults/main/bsd.yml):** BSD installation variables

Dependencies
------------

None

Example Playbook
----------------

This is a sample playbook file for deploying the Ansible Galaxy NGINX App Protect role in a localhost and installing NGINX App Protect on NGINX Plus.

```yaml
---
- hosts: localhost
  become: true
  roles:
    - role: nginxinc.nginx_app_protect
```

This is a sample playbook file for deploying the Ansible Galaxy NGINX App Protect role to a dynamic inventory containing the `nginx_plus` tag.

```yaml
---
- hosts: tag_nginx_plus
  remote_user: root
  roles:
    - role: nginxinc.nginx_app_protect
```

To run any of the above sample playbooks create a `setup-nginx-app-protect.yml` file and paste the contents. Executing the Ansible Playbook is then as simple as executing `ansible-playbook setup-nginx.yml`.

Alternatively, you can also clone this repository instead of installing it from Ansible Galaxy. If you decide to do so, replace the role variable in the previous sample playbooks from `nginxinc.nginx_app_protect` to `ansible-role-nginx-app-protect`.

Other NGINX Roles
-----------------

You can find an Ansible collection of roles to help you install and configure NGINX Controller [here](https://github.com/nginxinc/ansible-collection-nginx_controller)

License
-------

[Apache License, Version 2.0](LICENSE)

Author Information
------------------

[Daniel Edgar](https://github.com/aknot242)

&copy; [F5 Networks, Inc.](https://www.f5.com/) 2020
