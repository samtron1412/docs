[TOC]

# Overview
A `chroot` on UNIX operating system is an operation that changes the apparent root directory for the current running process and its children.

A program that is run in such a modified environment cannot name (and therefore normally cannot access) files outside the **designated directory tree**. The modified environment is called a **chroot jail**.

## History
The chroot system call was introduced during development of Version 7 Unix in 1979, and added to BSD by Bill Joy on 18 March 1982.

An early use of the term **jail** as applied to chroot comes from Bill Cheswick in 1991.

To make it useful for virtualization, FreeBSD expanded the concept and in its 4.0 release in 2000 introduced the `jail` command.

By 2004 this had led to the coining of the term **jailbreak** (a jailbreak is the act or tool is used to perform the act of breaking out of a chroot or jail in UNIX-like operating systes or bypassing digital rights management (DRM)).

In 2005, Sun released Solaris Containers, described as **chroot on steroids**.

In 2008, LXC (kernel's features: cgroups + namespaces) adopted the **container** terminology.

# References
1. [Chroot Wikipedia][1]
2. [Change root Arch Linux Wiki][2]

[1]: https://en.wikipedia.org/wiki/Chroot "Chroot Wikipedia"
[2]: https://wiki.archlinux.org/index.php/Change_root "Change root Arch Linux Wiki"
