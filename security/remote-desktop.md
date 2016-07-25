[TOC]

# Overview
Remote desktop software allow a personal computer's desktop environment to be run remotely on one system, while being displayed on a separate client device.

Remote desktop software captures the mouse and keyboard inputs from the local computer (client) and sends them to the remote computer (server). The remote computer in turn sends the display commands to the local computer.

# Protocols
- X Window System (X11) - a well-established cross-platform protocol.
- Remote Frame Buffer (RFB) - A framebuffer level cross-platform protocol that VNC is based on.
- SPICE (Simple Protocol for Independent Computing Environments) - remote-display system built for virtual environments.
- Remote Desktop Protocol (RDP) - a Windows-specific protocol.

# Software
- [Remmina][2]
- [SSH with X forwarding][3]
- [FreeRDP][4]
- [Vino - server only][5]
- [Vinagre - old][6]
- [Chrome Remote Desktop][7]

# Security
- Confidentiality: if software don't have built-in encryption, we need a VPN/SSH tunnel, or wrap the connection in SSL/TLS.

# References
1. [Remote desktop software - Wikipedia][1]

[1]: https://en.wikipedia.org/wiki/Remote_desktop_software "Remote desktop software"
[2]: https://en.wikipedia.org/wiki/Remmina "Remmina - Wikipedia"
[3]: https://en.wikipedia.org/wiki/Secure_Shell "SSH - Wikipedia"
[4]: https://github.com/FreeRDP/FreeRDP "FreeRDP - GitHub"
[5]: https://wiki.gnome.org/Projects/Vino "Vino - GNOME"
[6]: https://wiki.gnome.org/Apps/Vinagre "Vnagre - GNOME Extra"
[7]: https://en.wikipedia.org/wiki/Chrome_Remote_Desktop "Chrome Remote Desktop - Wikipedia"
