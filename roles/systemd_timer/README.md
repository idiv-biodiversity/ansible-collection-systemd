Ansible Role: systemd_timer
===========================

An Ansible role that configures and installs a **systemd timer**.


Table of Contents
-----------------

<!-- toc -->

- [Role Variables](#role-variables)
  * [Time Zone](#time-zone)
  * [NTP Servers](#ntp-servers)
  * [Remove Legacy Packages](#remove-legacy-packages)
- [Dependencies](#dependencies)
- [Example](#example)

<!-- tocstop -->


Role Variables
--------------

Name of the timer:

```
systemd_timer_name: foo
```

Whether to enable and start the timer:

```
systemd_timer_enable: yes
systemd_timer_start: yes
```

User, group and working directory:

```
systemd_timer_user: admin
systemd_timer_group: admin
systemd_timer_working_directory: /var/lib/admin
```

When to run the timer:

```
systemd_timer_on_calendar: daily

systemd_timer_on_active_sec: 60
systemd_timer_on_boot_sec: 60
systemd_timer_on_startup_sec: 60
systemd_timer_on_unit_active_sec: 60
systemd_timer_on_unit_inactive_sec: 60
```

Scripts to transfer from your `templates`:

```
systemd_timer_scripts:
  - src: timer-script.sh
    dest: /usr/sbin/timer-script
    may_fail: yes
  - src: other-script.sh
    dest: /usr/sbin/other-script
```

What to start (defaults to `dest`s of `systemd_timer_scripts`), needed e.g. if
you need to supply arguments:

```
systemd_timer_exec_start:
  - /usr/sbin/timer-script a
  - -/usr/sbin/timer-script may fail
  - /usr/sbin/timer-script b
```

Environment and limits:

```
systemd_timer_environment:
  - key: RUST_BACKTRACE
    value: 1

systemd_timer_limits:
  - name: NOFILE
    value: 8192
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


Example
-------

```yml
---

- name: install foo timer
  ansible.builtin.include_role:
    name: idiv_biodiversity.systemd.systemd_timer
    apply:
      tags:
        - foo-timer
  vars:
    systemd_timer_name: foo
    systemd_timer_scripts:
      - src: foo.sh
        dest: /usr/sbin/foo
    systemd_timer_on_calendar: daily
  tags:
    - foo-timer

...
```
