# Overview

- https://wayland.freedesktop.org/
- https://wiki.archlinux.org/title/Wayland
- Wayland is a replacement for the X11 window system protocol and
  architecture with the aim to be easier to develop, extend, and
  maintain.
- Wayland is the language (protocol) that applications can use to talk
  to a display server in order to make themselves visible and get input
  from the user (a person). A Wayland server is called a
  "compositor". Applications are Wayland clients.
- Wayland also refers to a system architecture. It is not just a
  server-client relationship between a compositor and
  applications. There is no single common Wayland server like Xorg is
  for X11, but every graphical environment brings with it one of many
  compositor implementations. Window management and the end user
  experience are often tied to the compositor rather than swappable
  components.
- A core part of Wayland architecture is libwayland: an inter-process
  communication library that translates a protocol definition in XML to
  a C language API. This library does not implement Wayland, it merely
  encodes and decodes Wayland messages. The actual implementations are
  in the various compositor and application toolkit projects.
- Wayland does not restrict where and how it is used. A Wayland
  compositor could be a standalone display server running on Linux
  kernel modesetting and evdev input devices or on many other operating
  systems, or a nested compositor that itself is an X11 or Wayland
  application (client). Wayland can even be used in application-internal
  communication as is done in some web browsers.

