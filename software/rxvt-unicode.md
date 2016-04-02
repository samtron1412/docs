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
