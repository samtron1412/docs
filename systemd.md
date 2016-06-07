[TOC]

# Overview


## Resources
- [Systemd for upstart user](https://wiki.ubuntu.com/SystemdForUpstartUsers)
- [systemd use guide](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units#editing-unit-files)

# Troubleshooting
## [/var stay busy at shutdown due to journald](https://github.com/systemd/systemd/issues/867)
- Fix by change `Storage=volatile` in `/etc/systemd/journald.conf`: journald will save log to `/run/log/journal` instead `/var/log/journal`

# Tips and Tricks
## [Allow user to shutdown](https://wiki.archlinux.org/index.php/Allow_users_to_shutdown)
Install `systemd-sysvcompat`
