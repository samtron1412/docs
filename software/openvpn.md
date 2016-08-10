[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/OpenVPN)
- [Arch Wiki](https://wiki.archlinux.org/index.php/OpenVPN)

OpenVPN is an open-source software application that implements virtual private network (VPN) techniques for creating secure point-to-point or site-to-site connections in routed or bridged configurations and remote access facilities. It uses a custom security protocol that utilizes SSL/TLS for key exchange. It is capable of traversing network address translators (NATs) and firewalls. It was written by **James Yonan** and is published under the GNU General Public License (GPL).

- Install `openvpn`
- Install `openresolv`
- Install script `update-resolve-conf.sh`

# Start manually
`openvpn <path/to/config/file>`

`openvpn /etc/openvpn/client.conf`
