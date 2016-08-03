[TOC]

# Overview
## What?
`systemd` is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as PID 1 and starts the rest of the system.

- provides aggressive parallelization capabilities
- uses socket and D-Bus activation for starting service
- offers on-demand starting of daemons
- keeps track of processes using Linux control groups
- supports snapshotting and restoring of the system state
- maintains mount and automount points
- implements an elaborate transactional dependency-based service control logic.
- supports SysV and LSB init scripts and works as a replacement for sysvinit.

**Other parts:**
- a logging daemon
- utilities to control basic system configuration like the hostname, date, locale, maintain a list of logged-in users and running containers and virtual machines, system accounts, runtime directories and settings
- daemons to manage simple network configuration, network time synchronization, log forwarding, and name resolution.

**License**: GNU Lesser General Public License (>=2.1)

**Spelling**: `systemd` - `System Five Hundred`

[Source](https://github.com/systemd/systemd)

## Why?


## Resources
- [Homepage](https://freedesktop.org/wiki/Software/systemd/)
- [Wikipedia](https://en.wikipedia.org/wiki/Systemd)
- [Archlinux Wiki](https://wiki.archlinux.org/index.php/Systemd)
- [Systemd for upstart user](https://wiki.ubuntu.com/SystemdForUpstartUsers)
- [systemd use guide](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units#editing-unit-files)
- [Linux Torvalds and others on Linux's systemd](http://www.zdnet.com/article/linus-torvalds-and-others-on-linuxs-systemd/)
- [The Biggest Myths](http://0pointer.de/blog/projects/the-biggest-myths.html)

# Design
## Unit files

## Core components and libraries

## Ancillary components

# Graphical frontends

# Forks and alternative implementations

# Tips and Tricks
## [Allow user to shutdown](https://wiki.archlinux.org/index.php/Allow_users_to_shutdown)
Install `systemd-sysvcompat`

# Troubleshooting
## [Debugging](https://freedesktop.org/wiki/Software/systemd/Debugging/)

## [/var stay busy at shutdown due to journald](https://github.com/systemd/systemd/issues/867)
- Fix by change `Storage=volatile` in `/etc/systemd/journald.conf`: journald will save log to `/run/log/journal` instead `/var/log/journal`

