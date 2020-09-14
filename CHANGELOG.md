# Changelog

## 0.2.0 (September 10, 2020)

BREAKING CHANGES:

*   All of the variables have been updated to prevent naming collisions when using other roles. Please see README.MD for new variable names.
*   Example playbook has been removed by collection authors in favor of using the Molecule configuration as a 'known-working' implementation.

ENHANCEMENTS:

*   Huge refactoring by @alessfg to better unify this role with the structures present in the other nginxinc Ansible roles.
*   Update Ansible to 2.9.13 and Ansible Lint to 4.3.4.
*   Explicitly defined mode in relevant tasks for breaking changes in Ansible.
*   Role refactored to separate install and configure operations in preparation for an upcoming role split.

FEATURES:

*   Molecule 3 testing foundation is in the project, and linting is being performed by TravisCI. Now time to write tests!

BUG FIXES:

*   The CentOS, RHEL, Debian and Ubuntu repositories have slightly changed to respond to a NAP repository deprecation activity. You may run into some duplication issues when running the role on a preexisting target that already has had NGINX installed using the role. To fix this, manually remove the old repository source.
*   The RHEL and CentOS repository setups were incorrectly using a static gpgkey instead of using the variable as a source.

## 0.1.0 (September 9, 2020)

Supports App Protect 2.0, which brings a number of features including support for Ubuntu 18.04.

Release notes for NGINX App Protect 2.0: docs.nginx.com/nginx-app-protect/releases/#release-2-0
