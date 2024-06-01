[TOC]

# Overview

- An Internet hosting service is a service that runs Internet servers,
  allowing organizations and individuals to serve content to the
  Internet.
- https://www.server-world.info/en/
    + How to manage servers?
- https://github.com/awesome-selfhosted/awesome-selfhosted
- https://github.com/awesome-foss/awesome-sysadmin

# Concepts and Common Terms

- https://wiki.r-selfhosted.com/learn/common-terms-and-concepts/

## Domain Names

- Basic concepts and details are in `dns.md`

## Certificates

- More details in `public-key-certificate.md`

## Host Types

### Colocation center

- Provide just the Internet connection, uninterrupted power and climate
  control, but let the client do his own system administration.

### Cloud hosting

- Which can also be termed time-share or on-demand hosting, in which the
  user only pays for the system time and space used, and capacity can be
  quickly scaled up or down as computing requirements change.

### Dedicated hosting

- The hosting service provider owns and manages the machine, leasing
  full control to the client.
- Management of the server can include monitoring to ensure the server
  continues to work effectively, backup services, installation of
  security patches and various levels of technical support.

### Virtual private server (VPS)

- Virtualization technology is employed in order to allow multiple
  logical servers to run on a single physical server.
- Common providers: try to find free credit from google search
    + AWS Lightsail
    + Linode
    + Digital Ocean
        * https://try.digitalocean.com/freetrialoffer/
    + Kamatera (HongKong)
    + Vultr
        * https://www.vultr.com/promo/try250/
        * https://help.cloud66.com/docs/cloud-66-101/free-vultr-credits

### Shared host

The server is shared. Sharing CPU, RAM, storage, bus interface,
bandwidth, etc.

### Your own servers

Buy your own servers and pay for dedicated Internet feeds with fixed IP
addresses.

# Software

## File synchronization

- Decentralized
    + https://github.com/syncthing/syncthing/
- Centralized
    + https://github.com/nextcloud/server
    + https://github.com/owncloud/core
    + https://github.com/haiwen/seafile

## Web servers

- nginx
- Apache

## Proxies

- `firewall.md` to learn more
- V2Ray
    + https://github.com/XTLS/Xray-core
    + Setup: https://youtu.be/V0YV0_n1-nI?si=P2W-xw9KteByHBi6
    + https://www.linuxbabe.com/ubuntu/set-up-v2ray-proxy-server
- shadowsocks
    + https://shadowsocks.org/
    + https://www.linode.com/docs/products/tools/marketplace/guides/shadowsocks/
- tinyproxy

## VPN servers

- Wireguard
    + https://www.linuxbabe.com/ubuntu/wireguard-vpn-server-ubuntu
- OpenConnect
    + https://www.linuxbabe.com/ubuntu/openconnect-vpn-server-ocserv-ubuntu-16-04-17-10-lets-encrypt
- OpenVPN
- SoftEtherVPN

## Email servers

- https://itsfoss.com/open-source-email-servers
- Issues with deliverability
    + https://www.reddit.com/r/selfhosted/comments/tuw8oi/where_to_host_vps_for_mail_server_or_are_days_of/
    + Limit spam: https://www.reddit.com/r/selfhosted/comments/t8gqir/comment/hzo8yhw/?utm_source=share&utm_medium=web2x&context=3
    + Sending out emails through services such as AWS SES, Mandrill, Mailgun, etc
    + Check deliverability of your email addresses
        * https://www.mail-tester.com/
        * https://mxtoolbox.com/blacklists.aspx
- mail in a box
    + https://mailinabox.email/
    + https://github.com/mail-in-a-box/mailinabox
- docker-mailserver
    + https://github.com/docker-mailserver/docker-mailserver
- mailcow
    + https://github.com/mailcow/mailcow-dockerized
    + https://docs.mailcow.email/
    + https://autoize.com/mailcow-managed-email-hosting/
- emailwiz
    + https://github.com/LukeSmithxyz/emailwiz
        * https://github.com/lukesmithxyz/mutt-wizard
- email alias
    + https://github.com/simple-login/app
- Hostinger cPanel to set up email server
    + https://www.hostinger.com/tutorials/how-to-host-your-own-email-server-on-a-vps-with-cyberpanel

# References

[1]: https://en.wikipedia.org/wiki/Internet_hosting_service "Wikipedia - Internet hosting service"
