Ansible Role: systemd_resolved
==============================

An Ansible role that configures **systemd-resolved**.

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

For a detailed description see `man 5 resolved.conf`.

Define your DNS servers:

```yml
systemd_resolved_servers:
  - a.b.c.1
  - a.b.c.2

systemd_resolved_fallback_servers:
  - d.e.f.1
  - d.e.f.2
```

Define your domains:

```yml
systemd_resolved_domains:
  - example.com
```

Other variables in the order they show up along with their default values:

```yml
systemd_resolved_dnssec: no
systemd_resolved_dns_over_tls: no
systemd_resolved_multicast_dns: yes
systemd_resolved_llmnr: yes
systemd_resolved_cache: yes
systemd_resolved_cache_from_localhost: no
systemd_resolved_dns_stub_listener: yes
systemd_resolved_dns_stub_listener_extra: ''
systemd_resolved_read_etc_hosts: yes
systemd_resolved_resolve_unicast_single_label: no
systemd_resolved_stale_retention_sec: 0
```


Dependencies
------------

```yml
---

# requirements.yml

collections:

  - name: ansible.posix

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
    - role: idiv_biodiversity.systemd.systemd_resolved
      tags:
        - systemd
        - systemd-resolved

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv_biodiversity.systemd.systemd_resolved
    tags:
      - systemd
      - systemd-resolved

...
```
