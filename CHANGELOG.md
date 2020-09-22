# Changelog

## 0.3.1 (Unreleased)

ENHANCEMENTS:

*   Split the default Molecule scenario into a simple and advanced scenario to solve timeout issues encountered in TravisCI.

BUG FIXES:

*   Rename handlers to use more specific role related naming and prevent namespace collision issues.
*   Add a `nginx_app_protect_service_modify` variable to revert a breaking change introduced in 0.3.0 where timeouts would not be set by default.
*   Set NGINX handler to `state: restarted` to prevent some compatibility issues when NGINX App Protect is installed on an instance already running NGINX beforehand.

## 0.3.0 (September 21, 2020)

DEPRECATION WARNING:

*   The ability to create an NGINX config including some basic App Protect directives has migrated to the NGINX config role available [here](https://github.com/nginxinc/ansible-role-nginx-config). Any new issues or PRs related to configuring NGINX App Protect directives should be submitted in the new NGINX Config repository. New issues or PRs related to configuring NGINX App Protect directives submitted in this repository will not be worked on. The NGINX App Protect directives configuration functionalities included in this role will be removed in an upcoming release.

FEATURES:

*   A new variable has been introduced:
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

*   Added molecule tests and verifications

BUG FIXES:

*   Fixed newly appearing linting issues in role

## 0.2.1 (September 11, 2020)

ENHANCEMENTS:

*   Bring docs up to speed with other NGINX roles
*   Move some default variables into the vars subfolder

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
