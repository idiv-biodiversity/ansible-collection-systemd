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

Role variables use the names of the `journald.conf` variables as documented in
`man 5 journald.conf`, prefixed with `systemd_journald_`, e.g.
`MaxRetentionSec` maps to `systemd_journald_maxretensionsec`.

**Note:** This role doesn't aim to be 100% complete at all times. When new
variables are introduced and you need them, feel free to contribute.


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
