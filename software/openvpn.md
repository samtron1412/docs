[TOC]

# Overview
OpenVPN is an open-source software application that implements virtual private network (VPN) techniques for creating secure point-to-point or site-to-site connections in routed or bridged configurations and remote access facilities. It uses a custom security protocol that utilizes SSL/TLS for key exchange. It is capable of traversing network address translators (NATs) and firewalls. It was written by **James Yonan** and is published under the GNU General Public License (GPL).

- Install `openvpn`
- Install `openresolv`
- Install script `update-resolve-conf.sh`

# Start manually
`openvpn <path/to/config/file>`

`openvpn /etc/openvpn/client.conf`

# Architecture
## Encryption
- OpenVPN uses the OpenSSL library to provide encryption of both the data and control channels.
- It can also use the HMAC packet authentication feature to add an additional layer of security to the connection.
- It can also use hardware acceleration to get better encryption performance.

## Authentication
- Pre-shared keys
- Certificate-based
- Username/password-based: depends on third-party modules

## Networking

## Security

## Extensibility

# References
1. [OpenVPN - Wikipedia][1]
2. [OpenVPN - Arch Wiki][2]

[1]: https://en.wikipedia.org/wiki/OpenVPN "OpenVPN - Wikipedia"
[2]: https://wiki.archlinux.org/index.php/OpenVPN "OpenVPN - Arch Wiki"
