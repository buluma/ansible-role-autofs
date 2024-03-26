# Ansible role [autofs](https://galaxy.ansible.com/ui/standalone/roles/buluma/autofs/documentation)

Install and configure autofs on your system.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-autofs/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-autofs/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-autofs.svg)](https://github.com/buluma/ansible-role-autofs/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-autofs.svg)](https://github.com/buluma/ansible-role-autofs/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-autofs.svg)](https://github.com/buluma/ansible-role-autofs/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/autofs)](https://galaxy.ansible.com/ui/standalone/roles/buluma/autofs/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-autofs/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: buluma.autofs
      autofs_maps:
        - mountpoint: /bind/mnt
          options:
            - "--timeout 60"
          directories:
            - path: mount
              server: ":/mnt"
              options:
                - "fstype=bind"
        - name: direct-mounts
          mountpoint: /-
          options:
            - "--timeout 60"
            - "--ghost"
          directories:
            - path: /bind/direct/mount
              server: ":/mnt"
              options:
                - "fstype=bind"
        - mountpoint: /do_not_exist
          state: absent
      nis_master_map: auto.master
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-autofs/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: false

  roles:
    - role: buluma.bootstrap
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-autofs/blob/master/defaults/main.yml):

```yaml
---
# defaults file for autofs

# The first slash in a path will be removed, all remaining slashes will be replaced with this character.
#   Example: mountpoint=/bin/mount & slash_replace_char="-"
#   Output file name: /etc/auto.bind-mount (leading slash removed, remaining replaced with "-")
slash_replace_char: ""

# Here you can configure automount mountpoints.
# autofs_maps:
#   - mountpoint: /home
#     directories:
#       - path: "*"
#         server: "server.example.com/&"
#   - mountpoint: /net
#     options:
#       - "--timeout=60"
#     directories:
#       - path: server
#         options:
#           - rw
#           - soft
#           - intr
#           - rsize=8192
#           - wsize=8192
#         server: "server.example.com:/"
#   - name: cifs-mounts  # optionally name the map (for use in files names).
#     mountpoint: /cifs
#     directories:
#       - path: data
#         options:
#           - fstype=cifs
#         server: "://server.example.com/sharename/"
#   - mountpoint: /fuse
#     directories:
#       - path: ftpserver
#         options:
#           - fstype=curl
#           - rw
#           - allow_others
#           - nodev
#           - nonempty
#           - noatime
#         server: ':ftp\://username\:password\@ftp.example.com'
#   - mountpoint: /do_not_exist
#     state: absent

# Set the nis_master_map.
# nis_master_map: auto.master
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-autofs/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-autofs/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Debian](https://hub.docker.com/r/buluma/debian)|bullseye|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|8|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[opensuse](https://hub.docker.com/r/buluma/opensuse)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|
|[Kali](https://hub.docker.com/r/buluma/kali)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-autofs/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-autofs/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-autofs/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)
