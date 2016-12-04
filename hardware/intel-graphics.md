[TOC]

# Overview

Since Intel provides and supports open source drivers, Intel graphics
are now essentially plug-and-play.

[List of Intel GPU][intel-gpu]

# Installation

- Install the `xf86-video-intel` package. It provides the **DDX** driver
  for 2D acceleration and it pulls in `mesa` as a dependency. Providing
  the **DRI** driver for 3D acceleration.
- To enable OpenGL support, also install `mesa-libgl`. If you need
  32-bit support, also install `lib32-mesa-libgl` from the `multilib`
  repository.
- For `Vulkan` support, install `vulkan-intel` for Ivy-Bridge or newer
  GPUs.

# Configuration

- There is no need for any configuration to run `Xorg`. However, to take
advantage of some driver options, you will need to create a Xorg
configuration file similar to the one below:
`/etc/X11/xorg.conf.d/20-intel.conf`

```
Section "Device"
	Identifier "Intel Graphics"
	Driver     "intel"
	Option "AccelMethod" "uxa"
EndSection
```

- Additional options are added by the user on new line below `Driver`.
- Using AccelMethod uxa because **sna** method sometimes cause problems

# Troubleshooting

## Chromium/Firefox problems

Set the AccelMethod to "uxa": `Option "AccelMethod" "uxa"`

# References

[intel-gpu]: https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "Wikipedia - Intel GPU"
