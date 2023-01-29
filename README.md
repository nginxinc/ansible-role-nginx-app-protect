[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx__app__protect-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx_app_protect)
[![Build Status](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect.svg?branch=main)](https://travis-ci.org/nginxinc/ansible-role-nginx-app-protect)
[![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# 👾 *Help make the NGINX App Protect Ansible role better by participating in our [survey](https://forms.office.com/Pages/ResponsePage.aspx?id=L_093Ttq0UCb4L-DJ9gcUKLQ7uTJaE1PitM_37KR881UM0NCWkY5UlE5MUYyWU1aTUcxV0NRUllJSC4u)!* 👾

# NGINX App Protect WAF and DoS Ansible Role <img src="images/nap-logo.png" width="30">

This role installs and configures NGINX App Protect WAF or DoS for NGINX Plus on your target host.

**Note:** By default, this role will install NGINX App Protect WAF. To install NGINX App Protect DoS, you need to set the `nginx_app_protect_dos_enable` variable to `true`.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

## Requirements

### NGINX App Protect

If you wish to install NGINX App Protect WAF or NGINX App Protect DoS using this role, you will need to obtain the corresponding NGINX App Protect license beforehand.

### Ansible

- This role is developed and tested with [maintained](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html) versions of Ansible core (above `2.12`).
- When using Ansible core, you will also need to install the following collections:

    ```yaml
    ---
    collections:
      - name: ansible.posix
        version: 1.4.0
      - name: community.crypto
        version: 2.10.0
      - name: community.general
        version: 6.2.0
      - name: community.docker  # Only required if you plan to use Molecule (see below)
        version: 3.4.0
    ```

    **Note:** You can alternatively install the Ansible community distribution (what is known as the "old" Ansible) if you don't want to manage individual collections.
- Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#upgrading-ansible-from-version-2-9-and-older-to-version-2-10-or-later).

### Jinja2

- This role uses Jinja2 templates. Ansible core installs Jinja2 by default, but depending on your install and/or upgrade path, you might be running an outdated version of Jinja2. The minimum version of Jinja2 required for the role to properly function is `3.1`.
- Instructions on how to install Jinja2 can be found in the [Jinja2 website](https://jinja.palletsprojects.com/en/2.11.x/intro/#installation).

### Molecule (Optional)

- Molecule is used to test the various functionalities of the role. The recommended version of Molecule to test this role is `4.x`.
- Instructions on how to install Molecule can be found in the [Molecule website](https://molecule.readthedocs.io/en/latest/installation.html). *You will also need to install the Molecule Docker driver.*
- To run the Molecule tests, you must copy your NGINX App Protect license to the role's [`files/license`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/files/license/) folder.

  You can alternatively add your NGINX App Protect repository certificate and key to the local environment. Run the following commands to export these files as base64-encoded variables and execute the Molecule tests:

  ```bash
  export NGINX_CRT=$( cat <path to your certificate file> | base64 )
  export NGINX_KEY=$( cat <path to your key file> | base64 )
  molecule test
  ```

## Installation

### Ansible Galaxy

To install the latest stable release of the role on your system, use:

```bash
ansible-galaxy install nginxinc.nginx_app_protect
```

Alternatively, if you have already installed the role, update the role to the latest release:

```bash
ansible-galaxy install -f nginxinc.nginx_app_protect
```

### Git

To pull the latest edge commit of the role from GitHub, use:

```bash
git clone https://github.com/nginxinc/ansible-role-nginx-app-protect.git
```

## Platforms

### NGINX App Protect WAF

The NGINX App Protect Ansible role supports all platforms supported by [NGINX Plus](https://www.nginx.com/products/technical-specs/) that intersect with the following list of distributions of App Protect WAF:

```yaml
Amazon Linux 2:
  - any
CentOS:
  - 7.4+
Debian:
  - buster (10)
RHEL:
  - 7.4+
  - 8.1+
Ubuntu:
  - bionic (18.04)
  - focal (20.04)
```

### NGINX App Protect DoS

The NGINX App Protect Ansible role supports all platforms supported by [NGINX Plus](https://www.nginx.com/products/technical-specs/) that intersect with the following list of distributions of App Protect DoS:

```yaml
Alpine:
  - 3.15
CentOS:
  - 7.4+
Debian:
  - buster (10)
  - bullseye (11)
RHEL:
  - 7.4+
  - 8.0+
Ubuntu:
  - bionic (18.04)
  - focal (20.04)
```

## Role Variables

This role has multiple variables. The descriptions and defaults for all these variables can be found in the **[`defaults/`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/defaults/)** folder in the following files:

| Name | Description |
| ---- | ----------- |
| **[`main.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/defaults/main.yml)** | NGINX App Protect installation and configuration variables |

Similarly, descriptions and defaults for preset variables can be found in the **`vars/`** folder in the following files:

| Name | Description |
| ---- | ----------- |
| **[`main.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/vars/main.yml)** | List of supported NGINX App Protect platforms |

## Dependencies

If NGINX Plus is *not* already installed on the system, this role will install the version of NGINX Plus that is dependent on the version of NGINX App Protect that is being installed.

## Example Playbook

A working functional playbook example can be found in the **`molecule/default/`** folder in the following file:

| Name | Description |
| ---- | ----------- |
| **[`molecule/default/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/molecule/default/converge.yml)** | Install and configure NGINX App Protect WAF |
 **[`molecule/advanced/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/molecule/advanced/converge.yml)** | Advanced integration test including NGINX App Protect WAF sending log data to a "remote" syslog server |
| **[`molecule/dos/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/molecule/dos/converge.yml)** | Install NGINX App Protect DoS |
| **[`molecule/specific-version/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/molecule/specific-version/converge.yml)** | Install a specific version of NGINX App Protect WAF signatures |
| **[`molecule/uninstall/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/molecule/uninstall/converge.yml)** | Uninstall NGINX App Protect WAF/DoS |

## Other NGINX Ansible Collections and Roles

You can find the Ansible NGINX Core collection of roles to install and configure NGINX Open Source, NGINX Plus, and NGINX App Protect WAF and DoS products [here](https://github.com/nginxinc/ansible-collection-nginx).

You can find the Ansible NGINX role to install NGINX OSS and NGINX Plus [here](https://github.com/nginxinc/ansible-role-nginx).

You can find the Ansible NGINX configuration role to configure NGINX [here](https://github.com/nginxinc/ansible-role-nginx-config).

You can find the Ansible NGINX Unit role to install NGINX Unit [here](https://github.com/nginxinc/ansible-role-nginx-unit).

## License

[Apache License, Version 2.0](https://github.com/nginxinc/ansible-role-nginx-app-protect/blob/main/LICENSE)

## Author Information

[Daniel Edgar](https://github.com/aknot242)

[Alessandro Fael Garcia](https://github.com/alessfg)

&copy; [F5, Inc.](https://www.f5.com/) 2020 - 2023
