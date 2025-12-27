[TOC]

# Overview

## What?

A virtual private network also known as a VPN is a private network that
extends across a public network or internet. It enables users to send
and receive data across shared or public networks as if their computing
devices were directly connected to the private network.

## Why?

Do we need VPNs?
- NO!!! with HTTPS
- https://youtu.be/9_b8Z2kAFyY?si=PhnTyiQJIYF6ByLt

VPNs can provide functionality, security and/or network management
benefits to the user.
- Some VPNs allow employees to securely access a corporate intranet
  while located outside the office.
- Some can securely connect geographically separated offices of an
  organization, creating one cohesive network.
- Individual Internet users can use some VPNs to secure their wireless
  transactions, to circumvent geo-restrictions and censorship, and/or to
  connect to proxy servers for the purpose of protecting personal
  identity and location.

# VPN prehistory

The first incentive to VPN creation was a desire of different companies
and corporations to remove a set of impediments of their successful
business development.

# Security mechanisms

VPNs cannot make online connections completely anonymous, but they can
usually increase privacy and security.

To prevent disclosure of private information, VPNs typically allow only
authenticated remote access using tunnelling protocols and encryption
techniques.

The VPN security model provides:
- **Confidentiality** such that even if the network traffic is sniffed
  at the packet level an attacker would only see encrypted data.
- Sender **authentication** to prevent unauthorized users from accessing
  the VPN.
- Message **integrity** to detect any instance of tampering with
  transmitted messages.

Secure VPN protocols include the following:
- **Internet Protocol Security (IPsec)** as initially developed by the
  Internet Engineering Task Force (IETF) for IPv6, which was required in
  all standards-compliant implementations of IPv6 before [RFC 6434][2]
  made it only a recommendation.
- **Secure Sockets Layer/Transport Layer Security (SSL/TLS)** can tunnel
  an entire network's traffic or secure an individual connection.
- **Point-to-Point Tunnelling Protocol (PPTP)**
- **Layer 2 Tunneling Protocol over IPsec (L2TP/IPsec)**
- Secure Shell (SSH) VPN - OpenSSH offers VPN tunnelling to secure
  remote connections to a network or to inter-network links.
- **Datagram Transport Layer Security (DTLS)** - used in Cisco
  AnyConnect VPN and in OpenConnect VPN to solve the issues SSL/TLS has
  with tunnelling over UDP.
- **Microsoft Point-to-Point Encryption (MPPE)** works with the
  Point-to-Point Tunnelling Protocol and in several compatible
  implementation on other platforms.
- **Microsoft Secure Socket Tunnelling Protocol (SSTP)** tunnels
  Point-to-Point Protocol (PPP) or Layer 2 Tunnelling Protocol traffic
  through an SSL 3.0 channel.
- Multi Path Virtual Private Network (MPVPN)

## Authentication

Tunnel endpoints must be authenticated before secure VPN tunnels can be
established.


# VPN protocols

- https://www.ivpn.net/en/pptp-vs-ipsec-ikev2-vs-openvpn-vs-wireguard/
- PPTP (old, legacy)
- IPSec with IKEv2
- OpenVPN
    + Can support both TCP and UDP transport protocols.
- Wireguard
    + Only support UDP

## UDP vs TCP

- https://airvpn.org/faq/udp_vs_tcp/
- UDP is a connectionless protocol, so during the handshake it is not
  always possible to do an effective error correction. As a result, when
  there's high ping or low quality line during the OpenVPN login, the
  handshake may fail, although you could see no significant problem
  after (if) the connection is established. TCP is capable of handling
  these problems.
- On the other hand, UDP is more efficient once the connection is
  established.
- If you experience problems with VoIP video/audio conversations when
  connected to the VPN through a TCP port, a typical case for which a
  difference may be visible (VoIP over TCP - for example UDP over TCP -
  is clearly inferior to VoIP over UDP because TCP implements ARQ, UDP
  does not), then go for an UDP connection.
- In general, you should always try an UDP connection if your ISP allows
  it and you don't experience any problem during the handshake.
- A particular case is a connection over TOR or over an http-proxy. In
  this case, TCP is mandatory.
- Variety of ports (53, 80, 443) is an additional option to try to
  bypass country or ISPs blocks, or bandwidth management.

## IPsec

- https://en.wikipedia.org/wiki/IPsec
- Old: L2TP (layer 2 tunneling protocol)
    + https://en.wikipedia.org/wiki/Layer_2_Tunneling_Protocol
- Newer: IKE (internet key exchange)
    + https://en.wikipedia.org/wiki/Internet_Key_Exchange

# VPN on routers

## [DD-WRT][3]

## [OpenWRT][4]

# References

1. [Virtual Private Network - Wikipedia][1]
2. [RFC 6434][2]
3. [DD-WRT][3]
4. [OpenWRT][4]

[1]: https://en.wikipedia.org/wiki/Virtual_private_network "Virtual Private Network - Wikipedia"
[2]: https://tools.ietf.org/html/rfc6434 "RFC 6434"
[3]: https://en.wikipedia.org/wiki/DD-WRT "DD-WRT"
[4]: https://en.wikipedia.org/wiki/DD-WRT "OpenWRT"
