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

## Configuration examples

- All configurations in this section are stored as `foo.network` in
`/etc/systemd/network`. For a full listing of options and processing
order, see [Configuration files](#configuration-files) and
`systemd-network(5)`.
- Systemd/udev automatically assigns predictable, stable network
interface
names for all local Ethernet, WLAN, WWAN interfaces. Use `networkctl
list` to list the devices on the system.
- After making changes to a configuration file, restart
`systemd-networkd.service`.

### Wired adapter using DHCP

`/etc/systemd/network/wired.network`

```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4
```

### Wired adapter using a static IP

`/etc/systemd/network/wired.network`

```
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1
```

- You may specify multiple IP addresses.
- Add an IPv6 address with another Address= line.
- See the `systemd.network(5)` man page for more network options such as
specifying DNS servers and a broadcast address.

### Wireless adapter

- In order to connect to a wireless network with systemd-networkd, a
wireless adapter configured with another service such as wpa_supplicant
is required.
- In this example, the corresponding systemd service file that needs to
be enabled is `wpa_supplicant@wlp2s0.service`. This service will run
wpa_supplicant with the configuration file
`/etc/wpa_supplicant/wpa_supplicant-wlp2s0.conf`. If this file does not
exist, the service will not start.

`/etc/systemd/network/wireless.network`

```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4
```

If the wireless adapter has a static IP address, the configuration is
the same as in a wired adapter.

### Wired and wireless adapters on the same machine

- The setup will enable a DHCP for both a wired and wireless connection
making use of the metric directive to allow the kernel to decide
on-the-fly which one to use. This way, no connection downtime is
observed when the wired connection is unplugged.
- The kernel's route metric (same as configured with ip) decides which
route to use for outgoing packets, in cases when several match. This
will be the case when both wireless and wired devices on the system have
active connections. To break the tie, the kernel uses the metric. If one
of the connections is terminated, the other automatically wins without
there being a gap with nothing configured.

`/etc/systemd/network/wired.network`

```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=10
```

`/etc/systemd/network/wireless.network`

```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=20
```

### Renaming an interface

- Instead of editing udev rules, a .link file can be used to rename an
interface.
- A useful exapmle is to set a predictable interface name for a
USB-to-Ethernet adapter based on its MAC address, as those adapters are
usually given different names depending on which USB port they are
plugged into.

`/etc/systemd/network/10-ethusb0.link`

```
[Match]
MACAddress=12:34:56:78:90:ab

[Link]
Description=USB to Ethernet Adapter
Name=ethusb0
```

Any user-supplied .link must have a lexically earlier file name than the
default config `99-default.link` in order to be considered at all. For
example, name the file `10-ethusb0.link` and not `ethusb0.link`.

# Configuration files

Configuration files are located in `/usr/lib/systemd/network`, the
volatile runtime network directory `/run/systemd/network` and the local
administration network directory `/etc/systemd/network`. Files in
`/etc/systemd/network` have the highest priority.

There are three types of configuration files. They all use a format
similar to systemd unit files.
- `.network` files. They will apply a network configuration for a
matching device.
- `.netdev` files. They will create a virtual network device for a
matching environment.
- `.link` files. When a network device appears, udev will look for the
first matching .link file.

They all follow the same rules:
- If all conditions in the `[Match]` section are matched, the profile
will be activated.
- An empty `[Match]` section means the profile will apply in any case
(can be compared to the `*` joker)
- All configuration files are collectively sorted and processed in
lexical order, regardless of the directory in which they live.
- Files with identical name replace each other.

## Tips
- To override a system-supplied file in `/usr/lib/systemd/network` in a
permanent manner (i.e. even after upgrade), place a file with same name
in `/etc/systemd/network` and symlink it to `/dev/null`.
- The `*` joker can be used in `VALUE` (e.g. `en*` match any Ethernet
device).
- Following this [arch-general thread][thread], the best practice is to
setup specific container network settings **inside the container** with
**networkd** configuration files.

# Usage with containers

# Management and desktop integration

# References

[awiki-systemd-networkd]: https://wiki.archlinux.org/index.php/Systemd-networkd "Arch Wiki: systemd-networkd"
[man-page]: https://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html "Systemd-networkd man page"
[thread]: https://lists.archlinux.org/pipermail/arch-general/2014-March/035381.html "[arch-general] tap device"
