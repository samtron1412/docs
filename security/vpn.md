[TOC]

# Overview
## What?
A virtual private network also known as a VPN is a private network that extends across a public network or internet. It enables users to send and receive data across shared or public networks as if their computing devices were directly connected to the private network.

## Why?
VPNs can provide functionality, security and/or network management benefits to the user.
- Some VPNs allow employees to securely access a corporate intranet while located outside the office.
- Some can securely connect geographically separated offices of an organization, creating one cohesive network.
- Individual Internet users can use some VPNs to secure their wireless transactions, to circumvent geo-restrictions and censorship, and/or to connect to proxy servers for the purpose of protecting personal identity and location.

# VPN prehistory
The first incentive to VPN creation was a desire of different companies and corporations to remove a set of impediments of their successful business development.

# Security mechanisms
VPNs cannot make online connections completely anonymous, but they can usually increase privacy and security.

To prevent disclosure of private information, VPNs typically allow only authenticated remote access using tunnelling protocols and encryption techniques.

The VPN security model provides:
- **Confidentiality** such that even if the network traffic is sniffed at the packet level an attacker would only see encrypted data.
- Sender **authentication** to prevent unauthorized users from accessing the VPN.
- Message **integrity** to detect any instance of tampering with transmitted messages.

Secure VPN protocols include the following:
- **Internet Protocol Security (IPsec)** as initially developed by the Internet Engineering Task Force (IETF) for IPv6, which was required in all standards-compliant implementations of IPv6 before [RFC 6434][2] made it only a recommendation.
- **Transport Layer Security (SSL/TLS)** can tunnel an entire network's traffic or secure an individual connection.
- Secure Shell (SSH) VPN - OpenSSH offers VPN tunnelling to secure remote connections to a network or to inter-network links.
- **Datagram Transport Layer Security (DTLS)** - used in Cisco AnyConnect VPN and in OpenConnect VPN to solve the issues SSL/TLS has with tunnelling over UDP.
- **Microsoft Point-to-Point Encryption (MPPE)** works with the Point-to-Point Tunnelling Protocol and in several compatible implementation on other platforms.
- **Microsoft Secure Socket Tunnelling Protocol (SSTP)** tunnels Point-to-Point Protocol (PPP) or Layer 2 Tunnelling Protocol traffic through an SSL 3.0 channel.
- Multi Path Virtual Private Network (MPVPN)

# References
1. [Virtual Private Network - Wikipedia][1]
2. [RFC 6434][2]

[1]: https://en.wikipedia.org/wiki/Virtual_private_network "Virtual Private Network - Wikipedia"
[2]: https://tools.ietf.org/html/rfc6434 "RFC 6434"
