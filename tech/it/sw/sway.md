# Overview

- A Wayland compositor (window manager + window compositor in X11).
- https://github.com/swaywm/sway/wiki
- Read i3 documentation carefully since sway is a replacement for i3 in
  wayland, so all the concepts should be the same:
    + https://i3wm.org/docs
    + https://i3wm.org/docs/userguide.html
    + Migration from i3 to sway
        * https://github.com/swaywm/sway/wiki/i3-Migration-Guide
- More sway documentation through man pages:
    + List of all sway docs: `man -k sway`
    + For example, configuration document: `man 5 sway`
- https://wiki.archlinux.org/title/Sway

# Tree / Concepts

- https://i3wm.org/docs/userguide.html#tree
- sway stores all layout info in a tree.
- The tree contains `containers`.
    + A `container` can host a window (application window that you can
      see and use) or  one/more containers.
- Orientation and split containers:
    + Every container has an orientation (horizontal, vertical or
      unspecified) and the orientation depends on the layout the
      container is in (vertical for splitv and stacking, horizontal for
      splith and tabbed).
    + You can change the orientation of a new container by using
      commands/shortcuts, and the next container will be in that
      orientation.
- Focus parent container by using `Mod + a`, then you can split this
  parent container using chosen orientation as explain above.
- Implicit containers
    + Some cases, implicit containers are created by sway to fulfill
      your command such as move windows around inside a workspace that
      changes the workspace orientation.
    + You can notice this in tabbed/stacking layout (e.g., "H[foot
      firefox]")
- Modes
    + Default (tiling)
    + Floating
    + Resize

# Additional Software

+ swaybg: wallpaper tool
+ swayidle: idle mangement daemon
+ swaylock: screen locker
+ swayimg: a lightweight image viewer
+ waybar: highly customizable status bar
    * https://github.com/Alexays/Waybar/wiki
    * alternatives: i3status
+ wf-recorder: screen recorder for wlroots-based compositors
+ sway-contrib: a collection of user-contributed scripts for sway
+ swaync: a simple GTK based notification daemon for Sway
    * alternatives: mako
+ nwg-displays: output management utility
+ swayosd: a GTK based on screen display for keyboard shortcuts
    * alternatives: wob


# Configuration

## Configure Keyboard Shortcuts

- https://wiki.archlinux.org/title/Sway#Keymap
- These keyboard shortcuts should be defined in `~/.config/sway/config`.
    + Search for `bindsym`
- General
    + `Mod + Enter`: new terminal
    + `Mod + d`: open dmenu (text based program launcher)
    + `Mod + Shift + q`: kill focused container (not closing the app if
      it has other windows in other containers)
    + `Mod + Ctrl + l`: lock screen
    + `Mod + Shift + e`: exit sway
    + `Mod + Shift + c`: reload sway configuration
- Scratchpad: a place to hold hidden containers
    + `Mod + Shift + -`: move container to scratchpad
    + `Mod + -`: show scratchpad and cycle through windows
- Moving around:
    + `Mod + h/j/k/l` or `Mod + <arrow_keys>`: move focus around
    + `Mod + Shift + h/j/k/l` or `Mod + Shift + <arrow_keys>`: move the
      focused window around
- Workspaces
    + `Mod + <number>`: switch to workspace
    + `Mod + Shift + <number>`: move focused container to workspace
- Layout
    + Orientation
        * `Mod + b`: split the current focused container horizontally
        * `Mod + v`: split the current focused container vertically
    + `Mod + f`: make the focused container fullscreen
    + `Mod + e`: default / toggle split (splith or splitv)
    + `Mod + s`: stacking
    + `Mod + w`: tabbed
    + `Mod + Shift + Space`: toggle between tiling and floating mode
    + `Mod + Space`: swap focus between tiling and floating area
    + `Mod + a`: move focus to parent container
    + `Mod + r`: enter resize mode
        * Using arrow keys or h/j/k/l keys to resize
        * Exit resize mode with Escape or Enter
- Screenshot
    + Full screen: `Print`
    + Select area: `Shift + Print`
    + Copy region to clipboard: `Ctrl + Print`
    + Select are, then annotate, then save: `Mod + Print`

## Output / Monitor / Display

- Show all output devices: `swaymsg -t get_outputs`
- Learn about supported configurations and how to configure:
    + `man sway-output`

## Execute External Commands

- `exec <command and options>`: only once when sway starts
- `exec_always <command and options>`: always execute each time the
  config is loaded.
- Sway will fork a new process to execute the command.

# Layout Saving and Restoring

- How to achieve saving and restoring layout similar to i3?
    + tmux helps with terminal layout, but this layout can be useful for
      other applications!
