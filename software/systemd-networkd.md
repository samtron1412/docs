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

There are three types of configuration files. They all use a format
similar to systemd unit files.
- `.network` files. They will apply a network configuration for a
matching device.
- `.netdev` files. They will create a virtual network device for a
matching environment.
- `.link` files. When a network device appears, udev will look for the
first matching .link file.

Configuration files are located in `/usr/lib/systemd/network`, the
volatile runtime network directory `/run/systemd/network` and the local
administration network directory `/etc/systemd/network`.
- All configuration files are collectively sorted and processed in
  lexical order, regardless of the directory in which they live.
- However, files with identical name replace each other. Files in /etc
  have the highest priority, files in /run take precedence over files
  with the same name in /usr/lib. This can be used to override a system-
  supplied configuration file withh a local file if needed. As a special
  case, an empty file (file size 0) or symlink with the same name
  pointing to `/dev/null` disables the configuration file entirely (it
  is "masked").
- If all conditions in the `[Match]` section are matched, the profile
  will be activated.
- An empty `[Match]` section means the profile will apply in any case
  (can be compared to the `*` joker)
- Along with the main configuration file, a **drop-in** directory (e.g.
  `/etc/systemd/network/foo.network.d/`) may exist. All files with the
  suffix **.conf** from this directory will be parsed after the file
  itself is parsed. This is useful to alter or add configuration
  settings, without having to modify the main configuration file. Each
  drop-in file must have appropriate section headers.

## Tips
- To override a system-supplied file in `/usr/lib/systemd/network` in a
  permanent manner (i.e. even after upgrade), place a file with same
  name in `/etc/systemd/network` and symlink it to `/dev/null`.
- The `*` joker can be used in `VALUE` (e.g. `en*` match any Ethernet
  device).
- Following this [arch-general thread][thread], the best practice is to
  setup specific container network settings **inside the container**
  with **networkd** configuration files.

## network files

These files are aimed at setting network configuration variables,
especially for servers and containers. `.network` files have the
following sections: `[Match]`, `[Link]`, `[Network]`, `[Address]`, `
[Route]` and `[DHCP]`. Below are commonly configured keys for each
section. See `systemd.network(5)` man page for more information and
examples.

### [Match]

A network file is said to match a device if each of the entries in the
"[Match]" section matches, or if the section is empty.

- `Name=` the device name
- `Host=` the machine hostname
- `Virtualization=` check whether the system is executed in a
virtualized environment or not. A `Virtualization=no` key will only
apply on your host machine, while `Virtualization=yes` apply to any
container or VM.

### [Link]

- `MACAddress=` useful for [MAC address spoofing][spoofing]
- `MTUBytes=` setting a larger MTU value ([jumbo frames][jumbo]) can
significantly speed up your network transfers

### [Network]

- `DHCP=` enables the DHCP client. Accepts "yes", "no", "ipv4" and
"ipv"6
- `DNS=` DNS server address
- `Bridge=` the bridge name
- `IPForward=` enables IP packet forwarding
- `Domains=` a list of domains to be resolved on this link

### [Address]

Specify several "[Address]" sections to configure several addresses.

`Address=` this option is **mandatory** unless DHCP is used

### [Route]

Specify several "[Route]" sections to configure several routes

`Gateway=` this option is mandatory unless DHCP is used

> **Tip**: you can put the `Address=` and `Gateway=` keys in the `
[Network]` section as a short-hand if `[Address]` section contains only
an Address key and `[Gateway]` contains only a Gateway key.

### [DHCP]

The "[DHCP]" section configures the DHCPv4 and DHCPv6 client, if it is
enabled with the `DHCP=` setting.

- `UseDomain=true`

## netdev files

These files will create virtual network devices. See `systemd.netdev(5)`
for more information and examples.

### Kinds of virtual network devices

| Kind      | Description                                                                                                                              |
| -         | -                                                                                                                                        |
| bond      | A bond device is an aggregation of all its slave devices. See [Linux Ethernet Bonding Driver HOWTO][bonding] for details.                |
| bridge    | A bridge device is a software switch, and each of its slave devices and the bridge itself are ports of the switch.                       |
| dummy     | A dummy device drops all packets sent to it.                                                                                             |
| gre       | A level 3 GRE tunnel over IPv4. See RFC 2784 for details.                                                                                |
| gretap    | A level 2 GRE tunnel over IPv4.                                                                                                          |
| ip6gre    | A level 3 GRE tunnel over IPv6.                                                                                                          |
| ip6tnl    | An IPv4 or IPv6 tunnel over IPv6.                                                                                                        |
| ip6gretap | A level 2 GRE tunnel over IPv6.                                                                                                          |
| ipip      | An IPv4 over IPv4 tunnel.                                                                                                                |
| ipvlan    | An ipvlan device is a stacked device which receives packets from its underlying device based on IP address filtering.                    |
| macvlan   | A macvlan device is a stacked device which receives packets from its underlying device based on MAC address filtering.                   |
| sit       | An IPv6 over IPv4 tunnel.                                                                                                                |
| tap       | A persistent level 2 tunnel between a network device and a device node.                                                                  |
| tun       | A persistent level 3 tunnel between a network device and a device node.                                                                  |
| veth      | An Ethernet tunnel between a pair of network devices.                                                                                    |
| vlan      | A VLAN is a stacked device which receives packets from its underlying device based on VLAN tagging. See [IEEE 802.1Q][vlan] for details. |
| vti       | An IPv4 over IPSec tunnel.                                                                                                               |
| vti6      | An IPv6 over IPsec tunnel.                                                                                                               |
| vxlan     | A virtual extensible LAN, for connecting Cloud computing deployments.                                                                    |
| vcan      | The virtual CAN driver. Similar to the network loopback devices, vcan offers a virtual local CAN interfaces.                             |

### [Match]

- `Host=`
- `Virtualization=`
- `KernelCommandLine=`
- `Architecture=`

### [Netdev]

- `Name=`: the interface name. This option is compulsory (mandatory)
- `Kind=`: the netdev kind (e.g. bond, bridge, vlan, etc.). This option
is mandatory.

## link files

These files are an alternative to custom udev rules and will be applied
by udev as the device appears. See `systemd.link(5)` for more
information and examples.

### [Match]

- `MACAddress=`
- `Host=`
- `Virtualization=`
- `Type=`

### [Link]

- `MACAddressPolicy=` persistent or random addresses
- `MACAddress=` a specific address

# Usage with containers

# Management and desktop integration

# References

[awiki-systemd-networkd]: https://wiki.archlinux.org/index.php/Systemd-networkd "Arch Wiki: systemd-networkd"
[man-page]: https://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html "Systemd-networkd man page"
[thread]: https://lists.archlinux.org/pipermail/arch-general/2014-March/035381.html "[arch-general] tap device"
[spoofing]: https://wiki.archlinux.org/index.php/MAC_address_spoofing "Arch Wiki - MAC address spoofing"
[jumbo]: https://wiki.archlinux.org/index.php/Jumbo_frames "Arch Wiki - Jumbo Frame"
[bonding]: https://www.kernel.org/doc/Documentation/networking/bonding.txt "Linux Ethernet Bonding driver HOWTO"
[vlan]: http://www.ieee802.org/1/pages/802.1Q.html "Virtual LANs"
