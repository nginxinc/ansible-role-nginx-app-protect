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

This role has multiple variables. The descriptions and defaults for all these variables can be found in the **[defaults/main.yml](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/defaults/main.yml)**.

Dependencies
------------

-   Since this role uses the [package_facts](https://docs.ansible.com/ansible/latest/modules/package_facts_module.html) module, on debian-based systems the `python-apt` package must be installed on targeted hosts.

-   If NGINX Plus is *not* already installed on the system, this role will install the version of NGINX Plus that is dependent on the version of NGINX App Protect set with the `nginx_app_protect_version` variable. If none is specified, the latest version of NGINX Plus and NGINX App Protect will be installed.

-   When using the `nginx_app_protect_version` variable, a specific version of NGINX Plus must already be installed on the target system.

Example Playbook
----------------

This is a sample playbook file for using the role to install NGINX App Protect on NGINX Plus and configure it using basic settings to all `wafs` inventory hosts.

A copy of this is in the sample-playbook directory in this repo.

First create a file for all the variables as `nginx-app-protect-vars.yml`

```yaml
---
# Specify whether you want to maintain your version of NGINX App Protect, upgrade to the latest version, or remove NGINX App Protect.
# Can be used with `nginx_app_protect_version` to achieve fine grained control on which version of NGINX App Protect is installed/used on each playbook execution.
# Using 'present' will install the latest version (or 'nginx_app_protect_version') of NGINX App Protect on a fresh install.
# Using 'latest' will upgrade NGINX App Protect to the latest version (that matches your 'nginx_app_protect_version') of NGINX App Protect on every playbook execution.
# Using 'absent' will remove NGINX App Protect from your system.
# Default is present.
nginx_app_protect_state: present

# OPTIONAL: Installs a specific version of NGINX App Protect
nginx_app_protect_version: 22

# The installation of NGINX App Protect includes a base signature set, which may be out of date.
# This option installs the latest NGINX App Protect signatures.
nginx_app_protect_install_signatures: true

# The installation of NGINX App Protect can include a page of frequently-updated, high-accuracy signatures called Threat Campaigns.
# This option installs the latest NGINX App Protect Threat Campaigns signatures.
nginx_app_protect_install_threat_campaigns: true

# Creates basic configuration files and enables NGINX App Protect on the target host
nginx_app_protect_configure: true

# Removes the license (certificate and key) for the NGINX App Protect repositories on the target host(s) when playbook run is complete.
nginx_app_protect_delete_license: true

# If you have a RHEL subscription, NGINX App Protect's dependencies will use subscription repos.
# Otherwise, it will source packages from CentOS' repositories.
nginx_app_protect_use_rhel_subscription_repos: false

# OPTIONAL: Choose where to fetch the NGINX App Protect and Security Updates signing keys from.
# Default settings are the official NGINX signing key hosts.
nginx_app_protect_signing_keys:
  nginx_plus: https://cs.nginx.com/static/keys/nginx_signing.key
  app_protect: https://cs.nginx.com/static/keys/app-protect.key
  security_updates: https://cs.nginx.com/static/keys/app-protect-security-updates.key

# For use with the nginx_app_protect_configure option to determine if the default security policy will be written to the target host
# Used when `nginx_app_protect_configure: true`.
nginx_app_protect_security_policy_template_enable: true

# Default app protect enforcement mode. Values can be `blocking` or `transparent`.
# Used when `nginx_app_protect_configure: true` and `nginx_app_protect_security_policy_template_enable: true`.
nginx_app_protect_security_policy_enforcement_mode: blocking

# For use with the nginx_app_protect_configure option to determine if the default log policy will be written to the target host.
# Used when `nginx_app_protect_configure: true`.
nginx_app_protect_log_policy_template_enable: true

# Which violation types to log. Possible values: all, illegal, blocked
# Used when `nginx_app_protect_configure: true` and `nginx_app_protect_log_policy_template_enable: true`.
nginx_app_protect_log_policy_filter_request_type: all

# For use with the nginx_app_protect_configure option to determine if the sample nginx.conf will be written to the target host.
# Since this can be dangerous, this value is default to false in the role defaults.
# Used when `nginx_app_protect_configure: true`.
nginx_app_protect_conf_template_enable: true

# For use with the nginx_app_protect_configure option to determine the syslog target to be injected
# into the default log policy that will be written to the target host.
# Used when `nginx_app_protect_conf_template_enable: true`.
nginx_app_protect_log_policy_syslog_target: 10.1.1.8:5144

# DEPRECATED: A proxy pass workload used in the sample nginx.conf for demo purposes.
# Will be removed from this role in the future.
# Used when `nginx_app_protect_conf_template_enable: true`.
nginx_app_protect_demo_workload: http://10.1.10.105:8080

# The location of the certificate and key to be used when downloading the packages onto the host.
nginx_app_protect_license:
  certificate: "{{ playbook_dir }}/license/nginx-repo.crt"
  key: "{{ playbook_dir }}/license/nginx-repo.crt"
```

This is a sample playbook file for deploying the Ansible Galaxy NGINX App Protect role in a localhost and installing NGINX App Protect on NGINX Plus.

```yaml
---
- hosts: wafs
  remote_user: centos
  pre_tasks:
  - name: load the vars
    include_vars:
      file: "{{ playbook_dir }}/nginx-app-protect-vars.yml"
  roles:
    - nginxinc.nginx_app_protect
```


To run any of the above sample playbooks create a `nginx-app-protect-playbook.yml` file and paste the contents. Executing the Ansible Playbook is then as simple as executing `ansible-playbook nginx-app-protect-playbook.yml -b -i inventory`.

Alternatively, you can also clone this repository instead of installing it from Ansible Galaxy. If you decide to do so, replace the role variable in the previous sample playbooks from `nginxinc.nginx_app_protect` to `ansible-role-nginx-app-protect`.

Other NGINX Roles
-----------------

You can find an Ansible collection of roles to help you install and configure NGINX Controller [here](https://github.com/nginxinc/ansible-collection-nginx_controller)

License
-------

[Apache License, Version 2.0](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/master/LICENSE)

Author Information
------------------

[Daniel Edgar](https://github.com/aknot242)

&copy; [F5 Networks, Inc.](https://www.f5.com/) 2020
