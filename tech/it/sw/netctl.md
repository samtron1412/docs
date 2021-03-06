[TOC]

# Overview

netctl is a CLI-based tool used to configure and manage network
connections via profiles.

# Usage

`man netctl`

# Configuration

netctl uses profiles to manage network connections and different modes
of operation to start profiles automatically or manually on demand.
- The netctl profile files are stored in `/etc/netctl/` and examples
  configuration files are available in `/etc/netctl/examples/`

# Tips and Tricks

- For wireless settings, you can use `wifi-menu -o` as root to generate
  the profile in `/etc/netctl/`

# References

[1]: https://wiki.archlinux.org/index.php/Netctl "Arch Wiki - netctl"
