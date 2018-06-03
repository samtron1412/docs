[TOC]

# Overview

In computing, virtualization refers to the act of creating a virtual
(rather than actual) version of something, including virtual computer
hardware platforms, operating systems, storage devices, and computer
network resources.

Virtualization began in the 1960s, as a method of logically dividing the
system resources provided by mainframe computers between different
applications.

# Classification

## Hardware virtualization

- Native: (kernel level) KVM, Xen
- Independent: (Standalone software) QEMU, VirtualBox

## OS-level virtualization

- docker
- lxc (cgroups, Linux namespaces)
- rkt
- systemd-nspawn

# Related software

- libvirt: virtualization management library

# References

1. [Virtualization Wikipedia][1]

[1]: https://en.wikipedia.org/wiki/Virtualization "Virtualization Wikipedia"
[qemu-kvm]: https://stackoverflow.com/questions/10307323/whats-the-differences-between-xen-qemu-and-kvm
[qemu-kvm-1]: https://serverfault.com/questions/208693/difference-between-kvm-and-qemu
[docker-lxc-lxd]: https://unix.stackexchange.com/questions/254956/what-is-the-difference-between-docker-lxd-and-lxc
[rkt-others]: https://coreos.com/rkt/docs/latest/rkt-vs-other-projects.html
[systemd-nspawn]: https://www.youtube.com/watch?v=s7LlUs5D9p4
[lxc-sec]: http://mattoncloud.org/2012/07/16/are-lxc-containers-enough/
[docker-sec]: https://blog.docker.com/2013/08/containers-docker-how-secure-are-they/
[systemd-vs-docker]: https://lwn.net/Articles/676831/
[systemd-vs-docker-1]: https://www.reddit.com/r/linux/comments/48m78l/systemd_vs_docker/
