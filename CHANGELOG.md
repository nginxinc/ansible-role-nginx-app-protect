# Changelog

## 0.7.1 (February 16, 2022)

ENHANCEMENTS:

* Add signing keys to a unique NGINX keyring on Debian based systems.
* Bump the Ansible `community.general` collection to `4.4.0` and `community.docker` collection to `2.1.1`.

BUG FIXES:

License and keys should now be correctly setup when neither signatures or threat campaigns are installed.

## 0.7.0 (October 28, 2021)

BREAKING CHANGES:

Refactor how `nginx_app_protect_*_policy_file*` variables work. You can now specify a list of both `security` and `log` policies for both NGINX App Protect WAF and NGINX App Protect DoS.

BUG FIXES:

* Fix instances of `nginx_app_protect_license_status` being incorrectly set as `nginx_license_status` instead.
* Add NGINX App Protect DoS to the NAP uninstall tasks.

## 0.6.2 (October 25, 2021)

ENHANCEMENTS:

* Remove Alpine 3.10 from the list of supported platform for NAP (and from Molecule).
* Move non NGINX App Protect specific dependencies from the role into the Molecule Dockerfile.
* Change Dependabot frequency from daily to weekly.
* Minor touch-up of GitHub actions workflows.

BUG FIXES:

* NGINX App Protect WAF 3.6 has been released and with it comes support for NGINX Plus R25. Per last release's KNOWN ISSUES, NGINX App Protect DoS will still only work with NGINX Plus R24.
* Always update NGINX App Protect dependencies to the latest available version to avoid outdated dependency issues (e.g. outdated CA certificates).

## 0.6.1 (September 30, 2021)

KNOWN ISSUES:

As of the latest NGINX Plus release, R25, NGINX App Protect WAF/DoS will no longer install or work on R25 platforms. The only workaround at this time is to install NGINX Plus R24 before attempting to install NGINX App Protect WAF/DoS. This issue will be fixed in NGINX App Protect WAF 3.6, planned for release mid-October, and in the next release of NGINX App Protect DoS, also planned for release mid-October.

ENHANCEMENTS:

* Remove Debian Stretch from the list of supported platforms for NAP (and from Molecule).
* Update the Ansible `community.general` collection to `3.7.0`, `ansible.posix` collection to `1.3.0` and `community.docker` collection to `1.9.1`.

BUG FIXES:

Role was failing at license and repo removal step when using the default of `nginx_app_protect_remove_license: true`.

## 0.6.0 (July 13, 2021)

BREAKING CHANGES:

Remove deprecated variables mentioned in the `0.5.0` release. These involve templating variables for both NGINX App Protect configs and policy/security files. Please instead use the [NGINX config role](https://github.com/nginxinc/ansible-role-nginx-config) for this (and much more) functionality.

FEATURES:

* Add support for NGINX App Protect DoS (Denial of Service) product. The `nginx_app_protect_dos_enable` variable must be set to `true` in order to install NGINX App Protect DoS.
* Add support for NGINX App Protect WAF on Amazon Linux 2 (requires NGINX App Protect 3.3).
* Add a `nginx_app_protect_manage_repo` feature flag which can be used to disable NGINX App Protect repo management by this role.

ENHANCEMENTS:

* Replace Ansible base with Ansible core. Ansible core will be the "core" Ansible release moving forward from Ansible `2.11`.
* Update GitHub actions to add a workflow dispatch option.
* Update the Ansible `community.general` collection to `3.3.2` and `community.docker` collection to `1.8.0`.
* Replace "yes"/"no" boolean values with "true"/"false" to comply with YAML spec `1.2`.
* Update `nginx` role requirement in Molecule tests to `0.20.0`.

## 0.5.0 (May 12, 2021)

BREAKING CHANGES:

The NGINX App Protect repository has been updated. This might cause some issues when running the role on an instance that already has NGINX Plus or NGINX App Protect installed. **Starting with NGINX Plus R25, you will need to install NGINX Plus using release `0.5.0`. If you are trying to install R23, please use release `0.4.3`. NGINX Plus R24 should work with both release `0.4.3` and `0.5.0`.**

DEPRECATION WARNINGS:

* **The ability to create an NGINX config including some basic App Protect directives will be removed in the upcoming `0.6.0` release at some stage after June 2021.** Please use the [NGINX config role](https://github.com/nginxinc/ansible-role-nginx-config) instead for this (and much more) functionality. This will include the removal of the following variables: `nginx_app_protect_conf_template_enable`, `nginx_app_protect_conf_template`, `nginx_app_protect_demo_workload_protocol`, `nginx_app_protect_demo_workload_host`, `nginx_app_protect_log_policy_syslog_target`, `nginx_app_protect_log_policy_target`.

* **The ability to dynamically create App Protect security and log policies via Jinja2 templates will be removed in the `0.6.0` release at some stage after June 2021 due to relative inflexibility.** The `nginx_app_protect_security_policy_file_enable`, `nginx_app_protect_security_policy_file_*`, `nginx_app_protect_log_policy_file_enable` and `nginx_app_protect_log_policy_file_*` variables should be used instead of the following variables which are to be removed: `nginx_app_protect_security_policy_template_enable`, `nginx_app_protect_security_policy_template`, `nginx_app_protect_security_policy_enforcement_mode`, `nginx_app_protect_log_policy_template_enable`, `nginx_app_protect_log_policy_template`, `nginx_app_protect_log_policy_filter_request_type`.

FEATURES:

* Implement Release Drafter.
* Add warning re having to install NGINX Plus beforehand on Alpine distros if NGINX Plus releases a security patch.

ENHANCEMENTS:

* Changing the default policy directory from `/etc/nginx` to `/etc/app_protect/conf` to align with this change introduced in App Protect 3.2.
* Update Ansible base to `2.10.9`, Ansible Lint to `5.0.8`, yamllint to `1.26.1` and Docker Python SDK to `5.0.0`.
* Update the Ansible `community.general` collection to `3.0.2` and `community.docker` collection to `1.6.0`.

## 0.4.3 (April 6, 2021)

BREAKING CHANGES:

The `nginx_app_protect_version` variable has been removed, as it cannot be implemented fully on all platforms.

FEATURES:

* Add support for Dependabot.
* Replace Ansible community distribution with Ansible base and add the necessary extra collections as a dependency requirement. For reference, these are:

    ```yaml
    ---
    collections:
      - name: community.general
        version: 3.0.0
      - name: ansible.posix
        version: 1.2.0
    ```

* Explicitly list Jinja2 `2.11.3` as a requirement, as well as detail the minimum supported version (`2.11.x`).
* You can now specify an `nginx_app_protect_repository` for NGINX App Protect.
* You can now specify an `nginx_app_protect_security_updates_repository` for NGINX App Protect signatures and threat campaigns packages.
* You can now specify NGINX App Protect signatures and threat campaigns package versions using the `nginx_app_protect_signatures_version` and `nginx_app_protect_threat_campaigns_version` variables.

ENHANCEMENTS:

* Support for NGINX App Protect 3.1 -- Adds support for Debian 10, Ubuntu 20.04 and Alpine 3.10.
* Add test coverage for new platforms and testing scenario.
* Consolidate dependencies into a single tasks file.
* Remove requirement for `package_facts` module when using this role.
* Update Signatures repository URL.
* Update Ansible base to `2.10.7`, Ansible Lint to `5.0.6`, Molecule to `3.3.0`, yamllint to `1.26.0` and Docker Python SDK to `4.4.4`.
* Specify GitHub actions Ubuntu release.
* Minor GitHub template tweaks, including the creation of a SECURITY doc.
* Only run GitHub actions Galaxy CI/CD workflow when a new release is published.

KNOWN ISSUES:

Service manager support is not included in NGINX App Protect for Alpine. When using this role to install NGINX App Protect on Alpine, you will need to start the NGINX App Protect processes then reload NGINX Plus yourself in order for App Protect to function. You can use commands similar to what are contained in the `entrypoint.sh` script in the [NGINX App Protect Administration Guide](https://docs.nginx.com/nginx-app-protect/admin-guide/install/#docker-deployment-instructions) to accomplish this.

## 0.4.2 (January 11, 2021)

ENHANCEMENTS:

* Replace TravisCI with GitHub actions.
* Update Ansible base to `2.10.4`, Ansible to `2.10.5`, Molecule to `3.2.2` and Docker Python SDK to `4.4.1`.
* Update copyright notice.

BUG FIXES:

Specify default values for the `nginx_app_protect_license` dictionary.

## 0.4.1 (November 17, 2020)

ENHANCEMENTS:

Update Ansible (now Ansible base) to `2.10.3`, Ansible (now Ansible Community Distribution) to `2.10.3`, Ansible Lint to `4.3.7`, and Molecule to `3.1.5`.

## 0.4.0 (November 16, 2020)

DEPRECATION WARNINGS:

The ability to dynamically create App Protect security and log policies via Jinja2 templates will be removed in a future release, as they weren't used much due to relative inflexibility. The `nginx_app_protect_security_policy_file_enable`, `nginx_app_protect_security_policy_file_*`, `nginx_app_protect_log_policy_file_enable` and `nginx_app_protect_log_policy_file_*` variables should be used instead of the `nginx_app_protect_*_policy_template*` variables. These new variables have been introduced in this release.

ENHANCEMENTS:

* Add survey to README.
* Improve README structure and use tables where relevant.
* Update Ansible (now Ansible base) to `2.10.2`, Ansible (now Ansible Community Distribution) to `2.10.0`, and yamllint to `1.25.0`.
* Ability to deploy static security policy files via the `nginx_app_protect_security_policy_file_enable` and `nginx_app_protect_security_policy_file_*` variables. NOTE: `nginx_app_protect_configure` must be set to true.
* Ability to deploy static log policy files via the `nginx_app_protect_log_policy_file_enable` and `nginx_app_protect_log_policy_file_*` variables. NOTE: `nginx_app_protect_configure` must be set to true.
* Add CentOS/RHEL 7.9 to list of supported platforms.

## 0.3.2 (September 30, 2020)

BUG FIXES:

Prevent TravisCI from trying to build (and failing) NGINX App Protect images on external PRs.

## 0.3.1 (September 22, 2020)

FEATURES:

* Two new variables have been introduced:
  * `nginx_app_protect_service_modify` -- Setting this variable to true/false will determine whether the default service timeout value gets modified.
  * `nginx_app_protect_log_policy_target` -- This variable is intended as an eventual replacement for `nginx_app_protect_log_policy_syslog_target` and allows using different destinations for NGINX App Protect's log files.

ENHANCEMENTS:

Split the default Molecule scenario into a simple and advanced scenario to solve timeout issues encountered in TravisCI.

BUG FIXES:

* Rename handlers to use more specific role related naming and prevent namespace collision issues.
* Set NGINX handler to `state: restarted` to prevent some compatibility issues when NGINX App Protect is installed on an instance already running NGINX beforehand.
* Using `update_cache: true` by itself in the `apt` module is not always idempotent. Moved the NGINX App Protect installation task to a corresponding `apt` or `yum` module to avoid this scenario.

## 0.3.0 (September 21, 2020)

DEPRECATION WARNING:

The ability to create an NGINX config including some basic App Protect directives has migrated to the NGINX config role available [here](https://github.com/nginxinc/ansible-role-nginx-config). Any new issues or PRs related to configuring NGINX App Protect directives should be submitted in the new NGINX Config repository. New issues or PRs related to configuring NGINX App Protect directives submitted in this repository will not be worked on. The NGINX App Protect directives configuration functionalities included in this role will be removed in an upcoming release.

BREAKING CHANGES:

`nginx_app_protect_delete_license` has been renamed to `nginx_app_protect_remove_license`.

FEATURES:

A new variable has been introduced:

* `nginx_app_protect_setup_license` -- Determine whether you want to use this role to upload your NGINX App Protect license to your target host.

ENHANCEMENTS:

* Switch to using `ansible_facts` wherever possible.
* Simplified overall role structure by:
  * Reducing signing key setup tasks to a single file.
  * Merging all install steps to a single file.
* Added handlers to check for NGINX syntax validity and fail if any errors are detected.
* Update Ansible Lint to `4.3.5`.

## 0.2.2 (September 15, 2020)

ENHANCEMENTS:

Added molecule tests and verifications.

BUG FIXES:

Fixed newly appearing linting issues in role.

## 0.2.1 (September 11, 2020)

ENHANCEMENTS:

* Bring docs up to speed with other NGINX roles.
* Move some default variables into the vars subfolder.

## 0.2.0 (September 10, 2020)

BREAKING CHANGES:

* All of the variables have been updated to prevent naming collisions when using other roles. Please see README.MD for new variable names.
* Example playbook has been removed by collection authors in favor of using the Molecule configuration as a 'known-working' implementation.

FEATURES:

* Molecule 3 testing foundation is in the project, and linting is being performed by TravisCI. Now time to write tests!

ENHANCEMENTS:

* Huge refactoring by @alessfg to better unify this role with the structures present in the other nginxinc Ansible roles.
* Update Ansible to `2.9.13` and Ansible Lint to `4.3.4`.
* Explicitly defined mode in relevant tasks for breaking changes in Ansible.
* Role refactored to separate install and configure operations in preparation for an upcoming role split.

BUG FIXES:

* The CentOS, RHEL, Debian and Ubuntu repositories have slightly changed to respond to a NAP repository deprecation activity. You may run into some duplication issues when running the role on a preexisting target that already has had NGINX installed using the role. To fix this, manually remove the old repository source.
* The RHEL and CentOS repository setups were incorrectly using a static gpgkey instead of using the variable as a source.

## 0.1.0 (September 9, 2020)

Supports App Protect 2.0, which brings a number of features including support for Ubuntu 18.04.

Release notes for NGINX App Protect 2.0: docs.nginx.com/nginx-app-protect/releases/#release-2-0
