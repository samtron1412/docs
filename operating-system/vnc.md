[TOC]

# Overview
Virtual network Computing (VNC) is a graphical desktop sharing system that uses the [Remote Frame Buffer protocol (RFB)][2] to remotely control another computer. It transmits the keyboard and mouse events from one computer to another, relaying the graphical screen updates back in the other direction, over a network.

VNC is platform-independent.

# Operation
- The **VNC server** is the program on the machine that shares its screen. The server passively allows the client to take control of it.
- The **VNC client** (or viewer) is the program that watches, controls, and interacts with the server. The client controls the server.
- The **VNC protocol** [RFB protocol][2] is very simple, based on one graphic primitive from server to client ("Put a rectangle of pixel data at the specified X, Y position") and event messages from client to server.

- In the normal method, a viewer connects to a port on the server (default port 5900).
- Alternatively a browser can connect to the server (depending on the implementation, default port is 5800).
- A server can connect to a viewer in **listening mode** on port 5500. One advantage of listening mode is that the server site does not have to configure its firewall to allow access on port 5900 (or 5800); the onus is on the viewer, which is useful if the server site has no computer expertise, while the viewer user would be expected to be more knowledgeable.

# Security
Since VNC was originally developed for use within a LAN, there are security issues when used over the Internet. Solutions
- VPN/SSH tunnel
- Wrap all VNC traffic with TLS

# References
1. [Virtual Network Computing - Wikipedia][1]
2. [Remote Frame Buffer protocol - Wikipedia][2]

[1]: https://en.wikipedia.org/wiki/Virtual_Network_Computing "Virtual Network Computing - Wikipedia"
[2]: https://en.wikipedia.org/wiki/RFB_protocol "Remote Frame Buffer protocol - Wikipedia"
