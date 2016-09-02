[TOC]

# Overview
OpenVPN is an open-source software application that implements virtual private network (VPN) techniques for creating secure point-to-point or site-to-site connections in routed or bridged configurations and remote access facilities. It uses a custom security protocol that utilizes SSL/TLS for key exchange. It is capable of traversing network address translators (NATs) and firewalls. It was written by **James Yonan** and is published under the GNU General Public License (GPL).

## What is OpenVPN?
With OpenVPN, we can:
- Tunnel any IP subnetwork or virtual ethernet adapter over a single UDP or TCP port.
- Using all of the encryption, authentication, and certification features of the OpenSSL library to protect the private network's traffic as it transits the Internet.
- Choosing between static-key based conventional encryption or certificate-based public key encryption.
- Using static, pre-shared keys or TLS-based dynamic key exchange.
- Using real-time adaptive link compression and traffic-shaping to manage link bandwidth utilization.
- Tunneling networks whose public endpoints are dynamic such as DHCP or dial-in clients.
- Tunneling networks through connection-oriented stateful firewalls without having to use explicit firewall rules.
- Tunneling networks over NAT.
- Create secure ethernet bridges using virtual tap devices.

## Why OpenVPN?
- OpenVPN is easy to use.
- OpenVPN is built for portability.
- OpenVPN is fast.
- OpenVPN has been rigorously designed and tested to operate robustly on unreliable networks.
	+ A major design goal of OpenVPN is that it should be as responsive, in terms of both normal operations and error recovery, as the underlying IP layer that it is tunneling over.
	+ That means that if the IP layer goes down for 5 minutes, when it comes back up, tunnel traffic will immediately resume even if the outage interfered with a dynamic key exchange which was scheduled during that time.
- OpenVPN has been built with a strongly modular design.
	+ All of the crypto is handled by the OpenSSL library, and all of the IP tunneling functionality is provided through the TUN/TAP virtual network driver.
	+ The benefits of this modularity can be seen, for example, in the way that OpenVPN can be dynamically linked with a new version of the OpenSSL library and immediately have access to any new functionality provided in the new release. For example, when OpenVPN is built with the latest version of OpenSSL (0.9.7), it automatically has access to new ciphers such as AES-256 (Advanced Encryption Standard with 256 bit key) and the encryption engine capability of OpenSSL that allows utilization of special-purpose hardware accelerators to optimize encryption, decryption, and authentication performance.
- While OpenVPN provides many options for controlling the security parameters of the VPN tunnel, it also provides options for protecting the security of the server itself, such as:
	+ `--chroot` for restricting the part of the file system the OpenVPN daemon has access to.
	+ `--user and --group` for downgrading daemon privileges after initialization.
	+ `--mlock` to ensure that key material and tunnel data is never paged to disk where it might later be recovered.

## Community
- [Source code][7]
-

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

# IPSec or PPTP or OpenVPN
- There are three major families of VPN implementations in wide usage today: SSL, IPSec, and PPTP. OpenVPN is an SSL VPN and as such is not compatible with IPSec, L2TP, or PPTP.
- The IPSec protocol is designed to be implemented as a modification to the IP stack in kernel space, and therefore each operating system requires its own independent implementation of IPSec.
- The OpenVPN's user-space implementation allows portability across operating systems and processor architectures, firewall and NAT-friendly operation, dynamic address support, and multiple protocol support including protocol bridging.
- The PPTP protocol has some [security vulnerabilities][8].

# References
1. [OpenVPN - Wikipedia][1]
2. [OpenVPN - Arch Wiki][2]
3. [TCP meltdown problem][3]
4. [mlockall][4]
5. [Remote Authentication Dial-In User Service (RADIUS)][5]
6. [Related Projects][6]
7. [Source code][7]
8. [PPTP's security vulnerabilities][8]
9. [Understanding the User-Space VPN: History, Conceptual Foundations, and Practical Usage][9]
10. [OpenVPN and the SSL VPN Revolution][10]

[1]: https://en.wikipedia.org/wiki/OpenVPN "OpenVPN - Wikipedia"
[2]: https://wiki.archlinux.org/index.php/OpenVPN "OpenVPN - Arch Wiki"
[3]: http://sites.inka.de/bigred/devel/tcp-tcp.html "TCP meltdown problem"
[4]: http://www.opengroup.org/onlinepubs/009695399/functions/mlockall.html "mlockall"
[5]: https://en.wikipedia.org/wiki/RADIUS "Remote Authentication Dial-In User Service (RADIUS)"
[6]: https://community.openvpn.net/openvpn/wiki/RelatedProjects "Ralated Projects"
[7]: https://github.com/OpenVPN/openvpn "OpenVPN source code"
[8]: http://www.schneier.com/pptp.html "PPTP's security vulnerabilities"
[9]: https://openvpn.net/papers/BLUG-talk/ "Understanding the User-Space VPN: History, Conceptual Foundations, and Practical Usage"
[10]: https://www.sans.org/reading-room/whitepapers/vpns/openvpn-ssl-vpn-revolution-1459 "OpenVPN and the SSL VPN Revolution"
