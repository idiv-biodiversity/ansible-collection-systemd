Ansible Role: systemd_timesyncd
===============================

An Ansible role that configures **systemd-timesyncd**.


Table of Contents
-----------------

<!-- toc -->

- [Role Variables](#role-variables)
  * [Time Zone](#time-zone)
  * [NTP Servers](#ntp-servers)
  * [Remove Legacy Packages](#remove-legacy-packages)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)

<!-- tocstop -->

Role Variables
--------------

### Time Zone

Set the system time zone. There is no default. The prefix is `system_` on
purpose, so this variable can be used across different roles that also set the
time zone.

```yml
systemd_timesyncd_timezone: Europe/Berlin
```

### NTP Servers

NTP servers are the preferred servers. They should be set to your networks
internal NTP servers.

```yml
systemd_timesyncd_ntp_servers:
  - ntp1.domain.org
  - ntp2.domain.org
  - ntp3.domain.org
```

Use regional pools for fallback servers:

```yml
systemd_timesyncd_ntp_fallback_servers:
  - 0.europe.pool.ntp.org
  - 1.europe.pool.ntp.org
  - 2.europe.pool.ntp.org
  - 3.europe.pool.ntp.org
```

### Remove Legacy Packages

Remove legacy timesync packages (ntp, chrony):

```yml
systemd_timesyncd_remove_legacy_packages: yes
```


Dependencies
------------

```yml
---

# requirements.yml

collections:

  - name: community.general

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
    - role: idiv_biodiversity.systemd.systemd_timesyncd
      tags:
        - systemd
        - systemd-timesyncd

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv_biodiversity.systemd.systemd_timesyncd
    tags:
      - systemd
      - systemd-timesyncd

...
```
