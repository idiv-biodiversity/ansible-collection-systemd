Ansible Role: systemd_networkd
==============================

An Ansible role that configures **systemd-networkd**.

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

For a detailed description see `man 5 systemd.network`.

**Note:** This role doesn't aim to be 100% complete at all times. When new
variables are introduced and you need them feel free to contribute.

```yml
---
# host_vars/my-client/vars.yml

systemd_networkd_networks:

  - name: 20-wired-static
    match:
      name: en*
    network:
      address: a.b.c.d/24
      gateway: a.b.c.x
      dns:
        - a.b.c.y
        - a.b.c.z
      domains:
        - example.com
      llmnr: 'no'
      multicast_dns: 'no'
      ntp:
        - 1.ntp.example.com
        - 2.ntp.example.com
        - 3.ntp.example.com
        - 4.ntp.example.com

  - name: 50-wireless
    match:
      name: w*
    network:
      dhcp: ipv4
      link_local_addressing: ipv4
    dhcp:
      route_metric: 20

...
```


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
    - role: idiv_biodiversity.systemd.systemd_networkd
      tags:
        - systemd
        - systemd-networkd

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv_biodiversity.systemd.systemd_networkd
    tags:
      - systemd
      - systemd-networkd

...
```
