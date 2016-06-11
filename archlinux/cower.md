[TOC]

# Overview

# cowerd (script use cower to install software)
```bash
#!/bin/sh
# install AUR packages with cower

cd $HOME/aur && cower -df "$1"
builddir="$_"
cd "$builddir" && ${EDITOR:-vim} PKGBUILD

makepkg -si && cd - &>/dev/null
```
