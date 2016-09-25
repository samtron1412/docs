[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/X_resources)
- [Arch Wiki](https://wiki.archlinux.org/index.php/X_resources)

In the X Window System, the X resources are parameters of X client applications. They are used in conjunction with or as an alternative to command line parameters and configuration files.

# Usage
## Load resource file
- Load a resource file (such as the conventional .Xresources), replacing any current settings: `$ xrdb ~/.Xresources`
- Load a resource file, and merge with the current settings: `$ xrdb -merge ~/.Xresources`
