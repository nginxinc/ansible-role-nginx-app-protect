Ansible NGINX Role
==================

<!-- [![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx) -->
<!-- [![Build Status](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect.svg?branch=master)](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect) -->

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
CentOS:
  versions:
    - 7.4
```

Role Variables
--------------

This role has multiple variables. The descriptions and defaults for all these variables can be found in the **[defaults/main.yml](./defaults/main.yml)`**.


Dependencies
------------

- Since this role uses the [package_facts](https://docs.ansible.com/ansible/latest/modules/package_facts_module.html) module, on debian-based systems the `python-apt` package must be installed on targeted hosts.

- NGINX+ R18-R20 must already be installed on the target system 

Example Playbook
----------------


This is a sample playbook file for using the role to install NGINX App Protect on NGINX Plus and configure it using basic settings to all `wafs` inventory hosts.

```yaml
---
- hosts: wafs
  become: true
  vars:
    # Installs NGINX App Protect and all dependencies to the target host
    app_protect_install: true

    # Creates basic configuration files and enables NGINX App Protect on the target host
    app_protect_configure: true

    # For use with the app_protect_configure option to determine if the default security policy will be written to the target host
    app_protect_security_policy_template_enable: true

    # For use with the app_protect_configure option to determine if the default log policy will be written to the target host
    app_protect_log_policy_template_enable: true

    # For use with the app_protect_configure option to determine if the sample nginx.conf will be written to the target host. 
    # Since this can be dangerous, this value is default to false in the role defaults
    nginx_conf_template_enable: true

    # For use with the app_protect_configure option to determine the syslog target to be injected 
    # into the default log policy that will be written to the target host
    log_policy_syslog_target: 10.1.1.8:5144

  roles:
    - role: ansible-role-nginx-app-protect
```

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
