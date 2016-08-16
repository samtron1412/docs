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
- OpenVPN can run over **User Datagram Protocol (UDP)** or **Transmission Control Protocol (TCP)** transports, multiplexing created SSL tunnels on a single TCP/UDP port.
- From 2.3.x version, OpenVPN fully supports IPv6 as protocol of the virtual network inside a tunnel and the OpenVPN applications can also establish connections via IPv6.
- It has the ability to work through most proxy servers (including HTTP) and Network address translation (NAT) and firewalls.
- The server configuration has the ability to push certain network configuration options to the clients.
	+ IP addresses
	+ routing commands
	+ a few connection options
- OpenVPN offers two types of interfaces for networking via the Universal TUN/TAP driver.
	+ It can create either a layer-3 based IP tunnel (TUN), or a layer-2 based Ethernet TAP that can carry any type of Ethernet traffic.
- Optionally use the LZO compression library to compress the data stream.
- Port 1194 is the official IANA assigned port number for OpenVPN.
- [TCP meltdown problem][3]

## Security
- It uses OpenSSL library.
- It runs in userspace, instead of requiring IP stack (therefore kernel) operation.
- It has the ability to drop root privileges
- Using [mlockall][4] to prevent swapping sensitive data to disk.
- Entering a chroot jail after initialization and apply a SELinux context after initialization.
- It runs a custom security protocol based on SSL and TLS rather than support IKE, IPsec, L2TP or PPTP.
- It offers support of smart cards via PKCS#11 based cryptographic tokens.

## Extensibility
- OpenVPN can be extended with third-party plugins or scripts which can be called at defined entry points.
- The purpose of this is often to extend OpenVPN with more advanced logging, enhanced authentication with username and passwords, dynamic firewall updates, [RADIUS][5] integration and so on.
- The plugins are dynamically loadable modules, usually written in C, while the scripts interface can execute any scripts or binaries available to OpenVPN.
- [Extensions][6]

# References
1. [OpenVPN - Wikipedia][1]
2. [OpenVPN - Arch Wiki][2]
3. [TCP meltdown problem][3]
4. [mlockall][4]
5. [Remote Authentication Dial-In User Service (RADIUS)][5]
6. [Related Projects][6]

[1]: https://en.wikipedia.org/wiki/OpenVPN "OpenVPN - Wikipedia"
[2]: https://wiki.archlinux.org/index.php/OpenVPN "OpenVPN - Arch Wiki"
[3]: http://sites.inka.de/bigred/devel/tcp-tcp.html "TCP meltdown problem"
[4]: http://www.opengroup.org/onlinepubs/009695399/functions/mlockall.html "mlockall"
[5]: https://en.wikipedia.org/wiki/RADIUS "Remote Authentication Dial-In User Service (RADIUS)"
[6]: https://community.openvpn.net/openvpn/wiki/RelatedProjects "Ralated Projects"
