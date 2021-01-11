# Changelog

## 0.4.2 (January 11, 2021)

ENHANCEMENTS:

*   Replace TravisCI with GitHub actions.
*   Update Ansible base to `2.10.4`, Ansible to `2.10.5`, Molecule to `3.2.2` and Docker Python SDK to `4.4.1`.
*   Update copyright notice.

BUG FIXES:

Specify default values for the `nginx_app_protect_license` dictionary.

## 0.4.1 (November 17, 2020)

ENHANCEMENTS:

Update Ansible (now Ansible base) to `2.10.3`, Ansible (now Ansible Community Distribution) to `2.10.3`, Ansible Lint to `4.3.7`, and Molecule to `3.1.5`.

## 0.4.0 (November 16, 2020)

DEPRECATION WARNING:

The ability to dynamically create App Protect security and log policies via Jinja2 templates will be removed in a future release, as they weren't used much due to relative inflexibility. The `nginx_app_protect_security_policy_file_enable`, `nginx_app_protect_security_policy_file_*`, `nginx_app_protect_log_policy_file_enable` and `nginx_app_protect_log_policy_file_*` variables should be used instead of the `nginx_app_protect_*_policy_template*` variables. These new variables have been introduced in this release.

ENHANCEMENTS:

*   Add survey to README.
*   Improve README structure and use tables where relevant.
*   Update Ansible (now Ansible base) to `2.10.2`, Ansible (now Ansible Community Distribution) to `2.10.0`, and yamllint to `1.25.0`.
*   Ability to deploy static security policy files via the `nginx_app_protect_security_policy_file_enable` and `nginx_app_protect_security_policy_file_*` variables. NOTE: `nginx_app_protect_configure` must be set to true.
*   Ability to deploy static log policy files via the `nginx_app_protect_log_policy_file_enable` and `nginx_app_protect_log_policy_file_*` variables. NOTE: `nginx_app_protect_configure` must be set to true.
*   Add CentOS/RHEL 7.9 to list of supported platforms.

## 0.3.2 (September 30, 2020)

BUG FIXES:

Prevent TravisCI from trying to build (and failing) NGINX App Protect images on external PRs.

## 0.3.1 (September 22, 2020)

FEATURES:

*   Two new variables have been introduced:
    *   `nginx_app_protect_service_modify` -- Setting this variable to true/false will determine whether the default service timeout value gets modified.
    *   `nginx_app_protect_log_policy_target` -- This variable is intended as an eventual replacement for `nginx_app_protect_log_policy_syslog_target` and allows using different destinations for NGINX App Protect's log files.

ENHANCEMENTS:

Split the default Molecule scenario into a simple and advanced scenario to solve timeout issues encountered in TravisCI.

BUG FIXES:

*   Rename handlers to use more specific role related naming and prevent namespace collision issues.
*   Set NGINX handler to `state: restarted` to prevent some compatibility issues when NGINX App Protect is installed on an instance already running NGINX beforehand.
*   Using `update_cache: true` by itself in the `apt` module is not always idempotent. Moved the NGINX App Protect installation task to a corresponding `apt` or `yum` module to avoid this scenario.

## 0.3.0 (September 21, 2020)

DEPRECATION WARNING:

The ability to create an NGINX config including some basic App Protect directives has migrated to the NGINX config role available [here](https://github.com/nginxinc/ansible-role-nginx-config). Any new issues or PRs related to configuring NGINX App Protect directives should be submitted in the new NGINX Config repository. New issues or PRs related to configuring NGINX App Protect directives submitted in this repository will not be worked on. The NGINX App Protect directives configuration functionalities included in this role will be removed in an upcoming release.

BREAKING CHANGES:

`nginx_app_protect_delete_license` has been renamed to `nginx_app_protect_remove_license`.

FEATURES:

A new variable has been introduced:
*   `nginx_app_protect_setup_license` -- Determine whether you want to use this role to upload your NGINX App Protect license to your target host.

ENHANCEMENTS:

*   Switch to using `ansible_facts` wherever possible.
*   Simplified overall role structure by:
    *   Reducing signing key setup tasks to a single file.
    *   Merging all install steps to a single file.
*   Added handlers to check for NGINX syntax validity and fail if any errors are detected.
*   Update Ansible Lint to `4.3.5`.

## 0.2.2 (September 15, 2020)

ENHANCEMENTS:

Added molecule tests and verifications.

BUG FIXES:

Fixed newly appearing linting issues in role.

## 0.2.1 (September 11, 2020)

ENHANCEMENTS:

*   Bring docs up to speed with other NGINX roles.
*   Move some default variables into the vars subfolder.

## 0.2.0 (September 10, 2020)

BREAKING CHANGES:

*   All of the variables have been updated to prevent naming collisions when using other roles. Please see README.MD for new variable names.
*   Example playbook has been removed by collection authors in favor of using the Molecule configuration as a 'known-working' implementation.

FEATURES:

*   Molecule 3 testing foundation is in the project, and linting is being performed by TravisCI. Now time to write tests!

ENHANCEMENTS:

*   Huge refactoring by @alessfg to better unify this role with the structures present in the other nginxinc Ansible roles.
*   Update Ansible to `2.9.13` and Ansible Lint to `4.3.4`.
*   Explicitly defined mode in relevant tasks for breaking changes in Ansible.
*   Role refactored to separate install and configure operations in preparation for an upcoming role split.

BUG FIXES:

*   The CentOS, RHEL, Debian and Ubuntu repositories have slightly changed to respond to a NAP repository deprecation activity. You may run into some duplication issues when running the role on a preexisting target that already has had NGINX installed using the role. To fix this, manually remove the old repository source.
*   The RHEL and CentOS repository setups were incorrectly using a static gpgkey instead of using the variable as a source.

## 0.1.0 (September 9, 2020)

Supports App Protect 2.0, which brings a number of features including support for Ubuntu 18.04.

Release notes for NGINX App Protect 2.0: docs.nginx.com/nginx-app-protect/releases/#release-2-0
