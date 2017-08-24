[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/Rxvt-unicode)
- [Arch wiki](https://wiki.archlinux.org/index.php/Rxvt-unicode)
- [Gentoo wiki](https://wiki.gentoo.org/wiki/Rxvt-unicode)

**rxvt-unicode**, commonly known as **urxvt**, is a customizable *terminal emulator* for the *X Window System*.

It was written by Marc Lehmann, who forked it from rxvt in November 2003.
- The capability to display different fonts and locales simultaneously and support for Unicode
- Resource-friendly like rxvt.
- Transparency
- Perl extensions
- Support for Xft fonts
- It has a daemon mode that reduces memory usage and loading time when using multiple terminals.

# Configuration
rxvt-unicode is controlled by **command-line arguments** or **Xresources**. Command-line arguments override, and take precedence over resource setting.

- `urxvt -help`: list options
- `urxvt --help`: list long-options

# Color
```
URxvt*background: black
URxvt*foreground: white
URxvt*color0: black
URxvt*color1: red3
URxvt*color2: green3
URxvt*color3: yellow3
URxvt*color4: blue2
URxvt*color5: magenta3
URxvt*color6: cyan3
URxvt*color7: gray90
URxvt*colorBD: grey50
URxvt*colorIT: red
URxvt*colorUL: green
URxvt*underlineColor: yellow
URxvt*highlightColor: blue
URxvt*highlightTextColor: magenta
URxvt*cursorColor: cyan
URxvt*cursorColor2: white
```

# Font

# Perl extensions
- [Source code](https://github.com/exg/rxvt-unicode/tree/master/src/perl)
- [URxvt Perl Extensions](http://jbl.web.cern.ch/jbl/doc/urxvt/)

## Common
- default

## Clickable URLs
You can make URLs in the terminal clickable using the **matcher** extension. For example, to open links in the chromium browser with the left mouse button, add the following to `.Xresources`:

	URxvt*perl-ext-common: default,matcher
	URxvt*url-launcher: /usr/bin/chromium
	URxvt*matcher.button: 1

Since rxvt-unicode 9.14, it's also possible to use matcher to open and list recent (currently limited to 10) URLs via keyboard:

	URxvt.keysym.C-Delete: perl:matcher:last
	URxvt.keysym.M-Delete: perl:matcher:list

Matching links can be colored with a chosen foreground or background color, for example blue:

	URxvt.matcher.rend.0: Uline Bold fg5

Matcher select mode, use up and down arrow key to select URLs.

	URxvt.keysym.C-u: perl:matcher:select

## [Changing font size on the fly](https://github.com/majutsushi/urxvt-font-size)

# Troubleshooting
## Remote hosts (ssh/chroot/systemd-nspawn)
If you are logging into a remote host (using SSH or chroot/systemd-nspawn), you may encounter problems when running text-mode programs under `rxvt-unicode-256color` or `rxvt-unicode`.
- This can be fixed by installing `rxvt-unicode-terminfo` on the remote host.
- Or by copying `/usr/share/terminfo/r/rxvt-unicode-256color` or `/usr/share/terminfo/r/rxvt-unicode` from your local machine to your host at `~/.terminfo/r`.
