[TOC]

# Eclipse plugin
WindowBuilder

# Design
## Top container
JFrame

JDialog

JApplet

## Layout
[GridBagLayout](http://www.formdev.com/jformdesigner/doc/layouts/gridbaglayout/), SpringLaout: dynamic and flexible.

## Enable, Disable element
- Enable: setEnabled(false)
- Disable: setEnabled(true)

**Note**: when add listener, must choose actionlister not choose mouselistener or anything. Because ActionListener at higher level compatible with setEnabled function.

## JFileChooser save last location
create JFileChooser variable at class scope (is an attribute of class)

