[TOC]

# Overview
- A router is a networking device that forwards data packets between computer networks.
- Routers perform the traffic directing functions on the Internet.
- A data packet is typically forwarded from one router to another through the networks that constitute the internetwork until it reaches its destination node.

# Open firmware
## [DD-WRT][2]
- [How to set-up DD-WRT][3]
- [A Definitive DD-WRT guide][4]

# Setup
## Dual gateway setup
Choose between local and VPN networks on a single router.
- Make a whitelist so only certain network devices connect through your VPN service.
- Create 2 WiFi networks; 1 for ISP network connections, and 1 for VPN network connections
- Filter only certain websites through your VPN connection (e.g. google.com) - Tomato firmware

## Dual router setup
Switch seamlessly between local and VPN network on any device, anytime. Using a new router for VPN network and keep the old router for the old network.

# References
1. [Wikipedia - Router][1]
2. [DD-WRT homepage][2]
3. [How to set-up DD-WRT][3]
4. [A Definitive DD-WRT guide][4]

[1]: https://en.wikipedia.org/wiki/Router_(computing) "Wikipedia - Router"
[2]: http://www.dd-wrt.com/site/index "DD-WRT homepage"
[3]: https://www.bestvpn.com/blog/9688/how-to-set-up-dd-wrt/ "How to set-up DD-WRT"
[4]: https://www.bestvpn.com/dd-wrt/ "A definitive DD-WRT guide"
