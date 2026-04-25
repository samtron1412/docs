# Overview

# Troubleshooting

## Ping and SSH work but sites aren't loading on browser

- https://www.reddit.com/r/WireGuard/comments/qmsa2n/ping_works_but_sites_arent_loading/
- Root cause details:
    + https://medium.com/@andreas.spanner/paying-attention-to-your-mtu-is-all-you-need-74e9b9d7d8e5
    + WireGuard sets "Don't Fragment (DF)" bit in IP header of outgoing
      packets (client to server) with the default MTU value 1500 bytes.
        * Then any device along the path with MTU smaller than the
          package will drop these packets and send back an ICMP
          Fragmentation Needed packet with the smaller MTU, so the
          client can adjust the MTU accordingly.
        * However, firewalls or security devices on the path between
          server and client can block the ICMP traffic, so the client
          will never adjust the new MTU and all the packets are drop by
          the devices with smaller MTU.
- Resolution
    + Setting MTU value in WireGuard configuration to a smaller
      conservative value such as 1280 for IPv6
- More details about MTU
    + https://en.wikipedia.org/wiki/Maximum_transmission_unit
    + https://en.wikipedia.org/wiki/Path_MTU_Discovery
- Example WireGuard configuration:

```
[Interface]
PrivateKey = <your-private-key>
Address = 10.0.0.2/32
DNS = 1.1.1.1
MTU = 1280
```
