rpmbuild
========

Ansible role which creates RPM build environment.


Examples
--------

```
---

# Example of basic usage
- hosts: myhost
  roles:
    - rpmbuild

# Example of how to change the default user
- hosts: myhost
  vars:
    rpmbuild_user_name: jdoe
    rpmbuild_user_home: /home/jdoe
  roles:
    - rpmbuild
```

This role requires [Config
Encoders](https://github.com/jtyr/ansible/blob/jtyr-config_encoders/lib/ansible/plugins/filter/config_encoders.py)
which must be configured in the `ansible.cfg` file like this:

```
[defaults]

filter_plugins = ./plugins/filter/
```

Where the `./plugins/filter/` containes the `config_encoders.py` file.


Role variables
--------------

List of variables used by the role:

```
# Package containing the RPM build tools
rpmbuild_pkg: rpm-build

# User under which the packages will be built
rpmbuild_user_name: root

# Home directory of the user
rpmbuild_user_home: /root

# Root of the build directory
rpmbuild_build_dir: "{{ rpmbuild_user_home }}/rpmbuild"

# RPM macros to be created in the user's directory
rpmbuild_macros:
  "%_topdir": "%(echo $HOME)/rpmbuild"
  "%dist": .el{{ ansible_distribution_major_version }}

# Directory structure to be created in the user's directory
rpmbuild_dirs:
  - "{{ rpmbuild_build_dir }}"
  - "{{ rpmbuild_build_dir }}/BUILD"
  - "{{ rpmbuild_build_dir }}/SOURCES"
  - "{{ rpmbuild_build_dir }}/SPECS"
  - "{{ rpmbuild_build_dir }}/SRPMS"
  - "{{ rpmbuild_build_dir }}/RPMS"
  - "{{ rpmbuild_build_dir }}/RPMS/noarch"
  - "{{ rpmbuild_build_dir }}/RPMS/{{ ansible_userspace_architecture }}"
```


Dependencies
------------

- [Config Encoders](https://github.com/jtyr/ansible/blob/jtyr-config_encoders/lib/ansible/plugins/filter/config_encoders.py)


License
-------

MIT


Author
------

Jiri Tyr
