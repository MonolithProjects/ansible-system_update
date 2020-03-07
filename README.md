System update
=========

<a href="https://galaxy.ansible.com/monolithprojects/system_update"><img src="https://img.shields.io/ansible/quality/46110?style=flat&logo=ansible"/></a> 
<a href="https://galaxy.ansible.com/monolithprojects/system_update"><img src="https://img.shields.io/ansible/role/d/46110"/></a> 
<a href="https://galaxy.ansible.com/monolithprojects/system_update"><img src="https://img.shields.io/github/v/release/MonolithProjects/ansible-system_update"/></a> 
<a href="https://github.com/MonolithProjects/ansible-system_update/actions"><img src="https://github.com/MonolithProjects/ansible-system_update/workflows/molecule%20test/badge.svg?branch=master"/></a>

This role will update all packages on RHEL/CentOS and Debian/Ubuntu systems.  
Optionally it can update the packages to specific distro release version (by default it is `latest`).
Another feature is the `smart reboot` where system will be rebooted after the package you specified in `smart_reboot_pkg:` list will be updated.

Requirements
------------

System must have access to the packages repository (Internet, Red Hat Satellite, etc.).


Role Variables
--------------

This is a copy from `defaults/main.yml`

```yaml
# Autoremove unused dependency packages for all modules.
autoremove_pkgs: no

# Reboot server if specific packages are updated
# smart_reboot_pkg:
#     - kernel
#     - dbus

# Specifies the Linux distro release from which all packages will be installed.
# By default the packages will be updated to the latest distro release.

# Debian or Ubuntu release version (example: xenial)
# deb_release_ver:

# RHEL/CentOS release version (example 6.10)
# el6_release_ver:

# RHEL/CentOS release version (exanple: 7.6.1810)
# el7_release_ver:

# RHEL/CentOS release version (example: 8.1.1911)
# el8_release_ver:
```

Example Playbook
----------------

Simple example. All packages will be updated to the latest version.

```yaml
---
- name: Example
  hosts: all
  become: true
  roles:
    - role: ansible-system_update
```

In this example `el7` system (RHEL7 or CentOS7) packages will be updated to the version same as for release `7.7.1908`. 
Using `autoremove_pkgs` the dependencies which are no longer needed will be autoremoved. 
System will be rebooted if `kernel` or `dbus` package is updated.  

```yaml
---
- name: Example
  hosts: all
  become: true
  vars:
    el7_release_ver: "7.7.1908"
    autoremove_pkgs: true
    smart_reboot_pkg:
      - kernel
      - dbus
  roles:
    - role: ansible-system_update
```

License
-------

MIT

Author Information
------------------

Created in 2020 by Michal Muransky