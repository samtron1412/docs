[TOC]

# Overview

- https://en.wikipedia.org/wiki/Computer_network
- Networking truths (12 of them)
    + https://datatracker.ietf.org/doc/html/rfc1925
- Internet Architectural Principles, Philosophy, and Guidelines
    + https://datatracker.ietf.org/doc/html/rfc1958
    + https://datatracker.ietf.org/doc/html/rfc3439
- Computer network
    + Origin: 1950s, Internet: 1970s
    + Network packet: control information + user data (payload)
    + Network topology: layouts (bus, star, etc.)
    + Network links:
        * Wired: coaxial cable, twisted pair, optical fiber
        * Wireless: microwave, radio wave, etc.
            - Protocols: bluetooth, wifi, NFC, etc.
    + Network nodes / devices
        * Network interface controllers (NIC)
        * Repeaters and Hubs
        * Bridges and Switches
        * Routers
        * Modems (modulate and demodulate)
    + Communication protocols
        * Internet protocol suite: TCP/IP
            - The foundation of all modern networking!
            - IP addresses.
            - TCP (connection-based) vs UDP (connectionless)
        * IEEE 802: local area networks (LAN) and metropolitan area
          networks (MAN)
            - Ethernet: IEEE 802.3, wired LANs
            - Wireless LANs: IEEE 802.11
        * Cellular standards
            - Global System for Mobile Communications (GSM)
            - Enhanced Data Rates for GSM Evolution (EDGE)
            - etc.
    + Open Systems Interconnection (OSI) model: conceptual model
        * https://en.wikipedia.org/wiki/OSI_model
    + Network performance
        * Bandwidth
        * Delay
        * Congestion, throughput, jitter, bit error rate, etc.
    + Security
        * End to end encryption (E2EE)
            - SSL/TLS
            - HTTPS
- Books and courses
    + UC Berkeley:
        + https://gaia.cs.umass.edu/kurose_ross/index.php
            * https://cs168.io/
            * https://www.youtube.com/watch?v=74sEFYBBRAY&list=PL1ya5dD_M8uX-BLUF1FEvUNsYWQL5_l0O
            * https://www.youtube.com/watch?v=BBzqX08GPo8&list=PLo80JwUm6hSSwGLJmS_quaeJgx9SILLiI
        + https://cs268.io/
    + Stanford: https://cs144.github.io/
    + https://www.amazon.com/TCP-Illustrated-Protocols-Addison-Wesley-Professional-dp-0321336313/dp/0321336313/ref=dp_ob_title_bk
    + Physical layer (lowest level in OSI model)
        * https://artofelectronics.net/
        * https://www.amazon.com/Digital-Signal-Processing-Communication-Systems/dp/0988873508


# TCP/IP Model / Internet Protocol Suite - This is the model with real world implementations!

- Foundational RFCs
    + Link, Internet, and Transport Protocols:
        * https://datatracker.ietf.org/doc/html/rfc1122
    + Application Protocols
        * https://datatracker.ietf.org/doc/html/rfc1122
- https://en.wikipedia.org/wiki/Internet_protocol_suite
    + The Internet protocol suite, commonly known as TCP/IP, is a framework for
      organizing the set of communication protocols used in the Internet and
      similar computer networks according to functional criteria.
    + The foundational protocols in the suite are the Transmission Control
      Protocol (TCP), the User Datagram Protocol (UDP), and the Internet
      Protocol (IP).
    + Early versions of this networking model were known as the Department of
      Defense (DoD) model because the research and development were funded by
      the United States Department of Defense through DARPA.
    + The Internet protocol suite provides end-to-end data communication
      specifying how data should be packetized, addressed, transmitted, routed,
      and received.
    + This functionality is organized into four abstraction layers, which
      classify all related protocols according to each protocol's scope of
      networking.
        * Application layer
            - https://en.wikipedia.org/wiki/Application_layer
            - Application message or stream of data
        * Transport layer
            - https://en.wikipedia.org/wiki/Transport_layer
            - UDP datagram or TCP segment / message
            - UDP: connectionless, packet switching
            - TCP: connection-oriented, virtual circuit switching
        * Internet / Network layer
            - https://en.wikipedia.org/wiki/Internet_layer
            - IP packet
        * Link / Network Interface layer
            - https://en.wikipedia.org/wiki/Link_layer
            - Ethernet frame.
        * Physical Network
            - Digital bits represented as analog signal (electromagnetic
              wave)
    + An implementation of the layers for a particular application forms a
      `protocol stack`.
- A TCP/IP tutorial
    + https://datatracker.ietf.org/doc/html/rfc1180 (READ THIS !!!)
    + A driver is software that communicates directly with the network
      interface hardware.
    + A module is software that communicates with a driver, with network
      applications, or with another module.
- Other resources
    + https://www.reddit.com/r/networking/comments/9fugxn/whats_the_difference_between_a_packet_and_a_frame/

# Open Systems Interconnection (OSI) Model - This is just a conceptual model without real implementation!

- https://en.wikipedia.org/wiki/OSI_model

# Transmission

- https://en.wikipedia.org/wiki/Packet_switching
- https://en.wikipedia.org/wiki/Circuit_switching
- Protocols
    + UDP: packet switching
    + TCP: virtual circuit switching
- Topology
    + https://en.wikipedia.org/wiki/Clos_network

# Network Nodes / Devices

- Typical modern home network

```
ISP -> phone / coaxial / optic line -> Modem -> Router [-> Repeater / Hub] -> Bridge / Switch / Wireless Access Point -> NIC -> Devices
```

Today, maybe one device can handle multiple functionalities
- Modem + Router + Switch + Wireless Access Point

## Modem

- https://en.wikipedia.org/wiki/Modem
- A modulator-demodulator, commonly referred to as a modem, is a
  computer hardware device that converts data between a digital format
  into a format suitable for an analog transmission medium such as audio
  wave or electromagnetic wave (electronic signal, light wave).
- A device that connects your home network to the Internet.
    + It actually connects to the phone line or the coaxial cable or
      whatever physical line you have.
    + It normally has at least an Ethernet connection, sometimes a USB
      as well.

- LAN: RJ45 jack (UTP cable + Ethernet port on modem)
- Phone line: RJ11 jack (DSL Cable + DSL port on modem)

## Router

- `router.md`
- A router is a networking device that forwards data packets between
  computer networks.
    + Routers perform the traffic directing functions on the Internet.
- A device that connects to the modem and allows multiple devices to use
  that internet connection at the same time.
    + It also lets the devices talk to each other (so you can transfer
      files in your house or whatever).
    + Can be wired, wireless, or both.
- All input output is RJ45 (WAN and LAN)

## Repeaters and Hubs

- Largely obsolete in today architecture! They are replaced by modern
  Switches.
    + https://www.reddit.com/r/networking/comments/uxumrv/hubs_where_are_they_still_used_why/
- https://en.wikipedia.org/wiki/Repeater
    + An electronic device that receives a signal and retransmits it.
    + Repeaters are used to extend transmissions so that the signal can
      cover longer distances or be received on the other side of an
      obstruction.
    + Some types of repeaters broadcast an identical signal, but alter
      its method of transmission, for example, on another frequency or
      baud rate.
- https://en.wikipedia.org/wiki/Ethernet_hub
    + An Ethernet hub, active hub, network hub, repeater hub, multiport
      repeater, or simply hub[a] is a network hardware device for
      connecting multiple Ethernet devices together and making them act
      as a single network segment.
    + It has multiple input/output (I/O) ports, in which a signal
      introduced at the input of any port appears at the output of every
      port except the original incoming.
    + A hub works at the physical layer (layer 1) in OSI model.

## Bridges and Switches

- https://en.wikipedia.org/wiki/Network_bridge
    + A network bridge is a computer networking device that creates a
      single, aggregate network from multiple communication networks or
      network segments.
    + Bridging is distinct from routing.
        * Routing allows multiple networks to communicate independently
          and yet remain separate, whereas bridging connects two
          separate networks as if they were a single network.
    + In the OSI model, bridging is performed in the data link layer
      (layer 2).
    + If one or more segments of the bridged network are wireless, the
      device is known as a wireless bridge.
- https://en.wikipedia.org/wiki/Network_switch
    + A network switch (also called switching hub, bridging hub,
      Ethernet switch, and, by the IEEE, MAC bridge) is networking
      hardware that connects devices on a computer network by using
      packet switching to receive and forward data to the destination
      device.
    + A network switch is a multiport network bridge that uses MAC
      addresses to forward data at the data link layer (layer 2) of the
      OSI model.
    + Some switches can also forward data at the network layer (layer 3)
      by additionally incorporating routing functionality.
        * Such switches are commonly known as layer-3 switches or
          multilayer switches

## Wireless Access Point

- https://en.wikipedia.org/wiki/Wireless_access_point
- Attaches to a router and allows wifi connections to the network.
- https://www.cisco.com/c/en/us/solutions/small-business/resource-center/networking/what-is-access-point.html

## Network Interface Controller (NIC)

- https://en.wikipedia.org/wiki/Network_interface_controller
- A network interface controller (NIC, also known as a network interface
  card, network adapter, LAN adapter and physical network interface) is
  a computer hardware component that connects a computer to a computer
  network.
- The network controller implements the electronic circuitry required to
  communicate using a specific physical layer and data link layer
  standard such as Ethernet or Wi-Fi.[a] This provides a base for a full
  network protocol stack, allowing communication among computers on the
  same local area network (LAN) and large-scale network communications
  through routable protocols, such as Internet Protocol (IP).

# Wired Network

## Ethernet

- https://en.wikipedia.org/wiki/Ethernet
- https://en.wikipedia.org/wiki/Terabit_Ethernet

## Fiber-optic communication

- https://en.wikipedia.org/wiki/Fiber-optic_communication

# Wireless Network

- Wireless Distribution System (WDS)
    + https://www.smallnetbuilder.com/wireless/wireless-howto/everything-you-need-to-know-about-wireless-bridging-and-repeating-part-1-wds/
    + https://kb.netgear.com/24106/What-is-a-wireless-distribution-system-and-how-does-it-work-with-my-Nighthawk-router
    + https://superuser.com/questions/362070/what-are-the-differences-between-a-repeater-bridge-and-wds
    + https://wiki.dd-wrt.com/wiki/index.php/Repeating_Mode_Comparisons
- Mesh wifi
    + https://www.reddit.com/r/HomeNetworking/comments/ikwtef/wds_mesh_or_what_else/

## Satellite Network

- SpaceX Starlink (2021)
- Amazon Kuiper

# WAN & LAN

1. Phân biệt việc kêt nối mạng cho wifi router vào port WAN hay port LAN
    - Gắn vào Port LAN thì sẽ phát cùng lớp mạng với nguồn cung cấp (vd:
      cùng lớp 192.168.1.0/24) cần phải tắt chế độ DHCP trên tất cả các
      con router wireless này
    - Gắn vào Port WAN: port WAN có 3 chế độ
        + **Bridge Mode** (giống hệt như gắn vào port LAN ít router hỗ trợ)
        + **DHCP client** chế độ này router wifi phải cấp DHCP lớp nào
          thì tùy bạn (vd: 192.168.12.0/24 cần phải khác với lớp được
          nhận từ WAN) tất cả user kết nối đến wifi router này đều đứng
          sau NAT tức là chỉ chia sẻ file với các user cùng kết nối
          chung SSID và router wireless nếu bạn không mở port
            * `192.168.12.3/24==>NAT==>192.168.1.6/24==>NAT==>180.148.4.6{Public IP}`
        + **Static IP** đặt IP cho WAN nếu bạn muốn quản lý nó dễ dàng hơn mọi thứ giống như DHCP client.

2. Lưu ý khi sử dụng nhiều router wireless để phủ sóng wifi
    - Cần phải xác định bạn có dùng phần mềm để quản lý băng thông hay
      phân quyền truy nhập gì không, có cần share file hay không. Có thì
      kết nối vào port LAN không cần thì kết nối vào WAN hay LAN gì cũng
      được. (nếu gắn vào LAN chú ý router chính cung cấp DHCP có đủ số
      lượng và ổn định không)
    - Router của bạn có tính năng WDS không. Nếu có có thể bật tính năng
      này lên và cấu hình cho các thiết bị cùng phát 1 SSID và Pass để
      di chuyển không phải gõ lại pass nhiều lần (nên tham khảo thêm tài
      liệu)
    - Quy hoạch sóng để tránh nhiễu ( 3 chanel không chồng lấn nhau là
      1,6,11)

# CIDR (Classless Inter-Domain Routing)

- https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing
- https://aws.amazon.com/what-is/cidr/

# Socket

- https://en.wikipedia.org/wiki/Network_socket
    + A network socket is a software structure (usually a triad of
      transport protocol, IP address, and port number) within a network
      node of a computer network that serves as an endpoint for sending
      and receiving data across the network.
    + The structure and properties of a socket are defined by an
      application programming interface (API) for the networking
      architecture.
- https://docs.oracle.com/javase/tutorial/networking/sockets/definition.html
    + A socket is one endpoint of a two-way communication link between
      two programs running on the network.
    + A socket is bound to a port number so that the TCP layer can
      identify the application that data is destined to be sent to.

# Power over

- Power over Ethernet (PoE)
    + https://en.wikipedia.org/wiki/Power_over_Ethernet
- Power over fiber
    + https://en.wikipedia.org/wiki/Power_over_fiber
- Power over LAN
    + https://en.wikipedia.org/wiki/Power_over_LAN

# Power-line communication (PLC) and Multimedia over Coax Alliance (MoCA)

- https://en.wikipedia.org/wiki/Power-line_communication
    + Power-line communication (PLC) is the carrying of data on a
      conductor that is also used simultaneously for AC electric power
      transmission or electric power distribution to consumers.
    + The line that does so is known as a power-line carrier.
- https://en.wikipedia.org/wiki/Multimedia_over_Coax_Alliance
    + The Multimedia over Coax Alliance (MoCA) is an international
      standards consortium that publishes specifications for networking
      over coaxial cable.
    + The technology was originally developed to distribute IP
      television in homes using existing cabling, but is now used as a
      general-purpose Ethernet link where it is inconvenient or
      undesirable to replace existing coaxial cable with optical fiber
      or twisted pair cabling.

# Data Over Cable Service Interface Specification (DOCSIS)

- https://en.wikipedia.org/wiki/DOCSIS
- Data Over Cable Service Interface Specification (DOCSIS) is an
  international telecommunications standard that permits the addition of
  high-bandwidth data transfer to an existing cable television (CATV)
  system.
    + It is used by many cable television operators to provide cable
      Internet access over their existing hybrid fiber-coaxial (HFC)
      infrastructure.
