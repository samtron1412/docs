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

## Why?


# Design
## Unit files

## Core components and libraries

## Ancillary components

# Graphical frontends

# Forks and alternative implementations

# Tips and Tricks
## [Allow user to shutdown][9]
Install `systemd-sysvcompat`

# Troubleshooting
## [Debugging][10]

## [/var stay busy at shutdown due to journald][11]
- Fix by change `Storage=volatile` in `/etc/systemd/journald.conf`: journald will save log to `/run/log/journal` instead `/var/log/journal`

# References
1. [Source Code][1]
2. [Homepage][2]
3. [Wikipedia][3]
4. [Archlinux Wiki][4]
5. [Systemd for upstart user][5]
6. [systemd use guide][6]
7. [Linux Torvalds and others on Linux's systemd][7]
8. [The Biggest Myths][8]
9. [Allow users to shutdown][9]
10. [systemd debugging][10]
11. [/var stay busy at shutdown due to journald][11]

[1]: https://github.com/systemd/systemd "Source Code"
[2]: https://freedesktop.org/wiki/Software/systemd/ "Homepage"
[3]: https://en.wikipedia.org/wiki/Systemd "Systemd - Wikipedia"
[4]: https://wiki.archlinux.org/index.php/Systemd "Systemd - Arch Wiki"
[5]: https://wiki.ubuntu.com/SystemdForUpstartUsers "Systemd for upstart users"
[6]: https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units "Systemd tutorials"
[7]: http://www.zdnet.com/article/linus-torvalds-and-others-on-linuxs-systemd/ "Linus Torvalds and others on Linux's systemd"
[8]: http://0pointer.de/blog/projects/the-biggest-myths.html "Systemd the biggest myths"
[9]: https://wiki.archlinux.org/index.php/Allow_users_to_shutdown "Allow users to shutdown"
[10]: https://freedesktop.org/wiki/Software/systemd/Debugging/ "Systemd debugging"
[11]: https://github.com/systemd/systemd/issues/867 "/var stay busy at shutdown due to journald"
