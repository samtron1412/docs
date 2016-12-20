[TOC]

# Overview

systemd-networkd is a system daemon that manages network
configurations.
- It detects and configures network devices as they
appear.
- It can also create virtual network devices.
- This service can be especially useful to set up complex network
configurations for a container managed by systemd-nspawn or for virtual
machines.

# Basic usage

## Required services and setup

To use systemd-networkd, start the following two services and enable
them to run on system boot:
- `systemd-networkd.service`
- `systemd-resolved.service`: this service is required only if you are
specifying DNS entries in `.network` files or if you want to obtain DNS
addresses from networkd's DHCP client.
    + For compatibility with resolv.conf, delete or rename the existing
    file and create the following symbolic link:
    + `# ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf`

# Configuration files

# Usage with containers

# Management and desktop integration

# References

[awiki-systemd-networkd]: https://wiki.archlinux.org/index.php/Systemd-networkd "Arch Wiki: systemd-networkd"
[man-page]: https://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html "Systemd-networkd man page"
