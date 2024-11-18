Ansible Role: systemd_journald
==============================

An Ansible role that configures **systemd-journald**.


Table of Contents
-----------------

<!-- toc -->

- [Role Variables](#role-variables)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)

<!-- tocstop -->

Role Variables
--------------

Role variables include journald configuration variables as documented in detail
at [freedesktop.org][freedesktop/journald] or `man 5 journald.conf`. Each role
variable has the `systemd_journald_` prefix, and is named accordingly, e.g.
`MaxRetentionSec=` maps to the `systemd_journald_maxretensionsec` role
variable.

**Note:** This role doesn't aim to be 100% complete at all times. When new
variables are introduced and you need them feel free to contribute.


Dependencies
------------

```yml
---

# requirements.yml

collections:

  - name: idiv_biodiversity.systemd
    version: X.Y.Z

...
```


Example Playbook
----------------

### Top-Level Playbook

Write a top-level playbook:

```yml
---

- name: head server
  hosts: head

  roles:
    - role: idiv_biodiversity.systemd.systemd_journald
      tags:
        - systemd
        - systemd-journald

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv_biodiversity.systemd.systemd_journald
    tags:
      - systemd
      - systemd-journald

...
```


[freedesktop/journald](https://www.freedesktop.org/software/systemd/man/journald.conf.html)
