[TOC]

# Overview

List of useful computer software.

# Internet

## Network managers

- [netctl][netctl]: Simple and robust tool to manage network connections
  via profiles. Intended to use with **systemd**.
- *systemd-networkd*: Native **systemd** daemon that manages network
  configurations. It includes support for basic network configurations
  through **udev**.

## Web browsers

- [Chromium](https://wiki.archlinux.org/index.php/Chromium)
- [Firefox](https://wiki.archlinux.org/index.php/Firefox)
- [w3m](https://en.wikipedia.org/wiki/W3m)
- [lynx](https://en.wikipedia.org/wiki/Lynx_(web_browser))
- [elinks](https://en.wikipedia.org/wiki/ELinks)
- [links](https://en.wikipedia.org/wiki/Links_(web_browser))
- [qutebrowser](https://github.com/qutebrowser/qutebrowser): vim-like
  browser
- [surf](https://surf.suckless.org/): one single C source file
- [surfer](https://github.com/nihilowy/surfer): simple browser for
  learning

## File sharing

- [uget](http://ugetdm.com/): GTK+ download manager

### BitTorrent

- [aria2](https://wiki.archlinux.org/index.php/Aria2): Lightweight
  download utility that supports simultaneous adaptive downloading via
  HTTP(S), FTP, BitTorrent protocols and Metalink.
- [deluge](https://wiki.archlinux.org/index.php/Deluge): User-friendly
  BitTorrent client written in PyGTK that can run as a daemon.

### FTP

- [filezilla](https://en.wikipedia.org/wiki/FileZilla): Fast and
  reliable FTP, FTPS and SFTP client.
- [proFTPd](https://wiki.archlinux.org/index.php/Proftpd): A secure and
  configurable FTP server. [Homepage](http://www.proftpd.org/)

## Communication

### Email clients

- [mutt](https://wiki.archlinux.org/index.php/Mutt): Small but very
  powerful text-based mail client. [Homepage](http://www.mutt.org/)
- [neomutt](https://github.com/neomutt/neomutt): Bringing together all
  the Mutt code

### IRC clients

- [weechat](https://en.wikipedia.org/wiki/WeeChat): Modular, lightweight
  ncurces-based IRC client.
- [irssi](https://wiki.archlinux.org/index.php/Irssi): Highly-
  configurable ncurses-based IRC client. [Homepage](http://irssi.org/)
- [hexchat](http://hexchat.github.io/): Fork of Xchat for Linux and
  Windows.

## News, RSS and blogs

- [newsbeuter](http://newsbeuter.org/): Ncurses RSS aggregator with
  layout and keybinding similar to the Mutt email client.
- [gpodder](http://gpodder.org/): a podcast client and feed aggregator
  (GTK+ and CLI).
- [greg](https://github.com/manolomartinez/greg): A command-line podcast
  aggregator.

### Reddit

- [rtv](https://github.com/michael-lazar/rtv): Browse Reddit from your
  terminal.
- [cortex](https://github.com/GGLucas/cortex): An ncurses Reddit browser
  and monitor.
- [cReddit](https://github.com/Cotix/cReddit): CLI Reddit client written
  in C.
- [alienfeed](https://github.com/jawerty/AlienFeed): Reddit CLI.

### Twitter

- [corebird](http://corebird.baedert.org/): Native GTK+ Twitter client
  for the Linux desktop.
- [pumpa](https://pumpa.branchable.com/): [pump.io](http://pump.io)
  client written in C++ and Qt.

### Hacker News

- Access hacker news or an unofficial alternative hacker news
  [interface](http://hckrnews.com/) by w3m/lynx.
- [haxor-news](https://github.com/donnemartin/haxor-news)
- [pyhn](https://github.com/socketubs/pyhn)
- [hn-cli](https://github.com/rafaelrinaldi/hn-cli)
- [vim-hackernews](https://github.com/ryanss/vim-hackernews)

### Usenet

- [slrn](https://en.wikipedia.org/wiki/slrn): An open source text-based
  news client. [Homepage](http://www.slrn.org/)
- [pan](https://en.wikipedia.org/wiki/Pan_(newsreader)): A GTK2 Usenet
  newsreader that's good at both text and binaries.
  [Homepage](http://pan.rebelbase.com/)
- [tin](https://en.wikipedia.org/wiki/Tin_(newsreader)): A cross-
  platform threaded NNTP and spool based Usenet newsreader.
  [Homepage](http://tin.org/)
- [nzbget](https://wiki.archlinux.org/index.php/NZBGet): CLI utility to
  grab Usenet binary file using .nzb files.
  [Homepage](http://nzbget.sourceforge.net/)
- [sabnzbd](sabnzbd.org)
- [lottanzb](http://www.lottanzb.org/)

### Blog

- `web-dev.md/Static-Site-Generator`

### Facebook Messenger

- [messengerfordesktop](https://github.com/Aluxian/Facebook-Messenger-Desktop)

## Bitcoin

## Cloud Computing

- OpenNebula
- CloudStack
- OpenStack

# Multimedia

## Codecs

## Image

### Image viewer

#### Graphical

- [sxiv](https://wiki.archlinux.org/index.php/Sxiv)
- [viewnior](https://www.archlinux.org/packages/?name=viewnior): use to
  view ico files
- [eog](https://www.archlinux.org/packages/?name=eog)
- [feh](https://wiki.archlinux.org/index.php/Feh)

#### Console

- [fbida](https://www.kraxel.org/blog/linux/fbida/)
- [fim](http://www.nongnu.org/fbi-improved/)
- [jfbview](http://seasonofcode.com/pages/jfbview.html)

### Image manipulation

#### Raster editors

- imagemagick
- graphicsmagick
- pinta: alternative for Paint.NET
- GIMP: alternative for Adobe Photoshop

#### Vector graphics - illustration

- Inkscape: alternative for Illustrator, CorelDraw
- yed: diagrams
- dia: diagrams

### Screen capture (screenshot)

- import command of imagemagick package
- [maim](https://github.com/naelstrof/maim)
- [screenfetch](https://github.com/KittyKatt/screenFetch)

### Optimize and Compress Images

- mogrify (ImageMagick)
    + `mogrify -quality 80 <file.jpg>`
- jpegoptim
    + `jpegoptim <file> --dest=/new/place`
    + `jpegoptim --size=200k <file> --dest=/new/place`
- optipng

## Audio

### Audio players

[mpd](https://wiki.archlinux.org/index.php/Music_Player_Daemon)
[mopidy](https://github.com/mopidy/mopidy)
[cmus](https://wiki.archlinux.org/index.php/Cmus)
[moc](https://wiki.archlinux.org/index.php/Moc)
[pianobar](https://wiki.archlinux.org/index.php/Pianobar)

### Audio tag editors

- [easytag](https://en.wikipedia.org/wiki/EasyTag)
- [puddletag](https://en.wikipedia.org/wiki/Puddletag)
- id3v2, id3

### Sound editor

- audacity

## Mobile phone managers

## Video

### Video players

- [mpv](https://wiki.archlinux.org/index.php/Mpv)
- [mplayer](https://wiki.archlinux.org/index.php/MPlayer)
- [smplayer](https://en.wikipedia.org/wiki/SMPlayer)
- [VLC](https://en.wikipedia.org/wiki/VLC_media_player)

### Subtitles

- aegisub: subtitle editor

### Video editors

- avidemux: free video editor designed for simple cutting, filtering and
  encoding tasks.
- handbrake: simple yet powerful video transcoder ideal for batch
  mkv/x264 ripping.

### Screencast

- obs: Free and open source software for video recording and live
  streaming
- asciinema: record your terminal in text base form

## Optical media burning

## Podcast

## Collection managers

## Lyrics fetchers

## YouTube utilities

- [you-get](https://www.archlinux.org/packages/community/any/you-get/)
- [youtube-dl](https://www.archlinux.org/packages/community/any/youtube-dl/)
- [clipgrab](https://www.archlinux.org/packages/community/x86_64/clipgrab/): a video downloader and converter
- [youtube-viewer](https://www.archlinux.org/packages/community/any/youtube-viewer/): a command line utility for viewing YouTube
- [mps-youtube](https://www.archlinux.org/packages/community/any/mps-youtube/): terminal base YouTube jukebox

## Others

- Rockbox: a free replacement firmware for digital music players

# Utilities

## Basic shell commands

## Build automation

## Terminal emulators

### Common

- [rxvt-unicode](https://wiki.archlinux.org/index.php/Rxvt-unicode)

### Windows

- [black-screen](https://github.com/black-screen/black-screen)
- babun (Windows)
- ConEmu (Windows)

### VTE-based

- VTE (Virtual Terminal Emulator) is a widget developed during early
  GNOME days for use in the GNOME terminal.
- [terminator](https://wiki.archlinux.org/index.php/Terminator)
- gnome-terminal
- guake
- lxterminal
- mate-terminal

### KMS-based

- The kernel mode setting
- They could be invoked without X
- kmscon

### framebuffer-based

- In GNU/Linux world, the framebuffer could be referred to a virtual
  device in the Linux kernel (fbdev) or the virtual framebuffer system
  for X (xvfb).
- This section mainly lists the terminal emulators that based on the in-
  kernel virtual device, i.e. fbdev
- yaft

## Disks

### Disk cleaning

- [bleachbit](http://www.bleachbit.org/)
- rmlint

### Disk usage display

- [ncdu](http://dev.yorhel.nl/ncdu)
- [baobab](https://wiki.gnome.org/Apps/Baobab)

### Partitioning tools

### Mount tools

- [udisks2](https://wiki.archlinux.org/index.php/Udisks)
- [udiskie](https://github.com/coldfix/udiskie)
- [udevil](https://www.archlinux.org/packages/?name=udevil)


## Files

### File Managers

[vifm](https://github.com/vifm/vifm)
[ranger](https://github.com/hut/ranger)

### File synchronization

### Archiving and compression tools

### Comparison, diff, merge

### Batch renames

### Search and replace

### Hashing

- https://github.com/gurnec/HashCheck (Windows)

## Keyboard and Typing

### Typing

- https://www.typing.com/student
- https://10fastfingers.com/
- play.typeracer.com
- https://www.typingclub.com/
- http://games.sense-lang.org/EN.php
- http://www.freetypinggame.net/play.asp
- http://www.how-to-type.com/

How to type fast:
- Touch typing (right typing technique)
    + No looking at the keyboard
    + Put hand at right position
- Familiar yourself with all the keys
- Aim for accuracy not speed at first
- Minimize physical effort
- Practice to build muscle memory


### Keyboard layout switchers

### Input methods

- GoTiengViet
- Unikey

## Clock synchronization

## System monitoring

- [progress](https://github.com/Xfennec/progress): Shows running
  coreutils basic commands and displays stats
- [netdata](https://github.com/firehol/netdata/wiki): A web-based real-
  time performance monitor.
- bootchart
- systemd-analyze

## System information viewers

- screenfetch
    + Show system information alongside the Arch Linux logo
- lshw
    + A small tool to provide detailed information on the hardware
      configuration of the machine with CLI and GTK interfaces.
- dmidecode (verbose and detail information)
    + It reports information about your system's hardware as described
      in your system BIOS according to the SMBIOS/DMI standard.
- hwinfo (probe hardware)
    + powerful hardware detection tool come from openSUSE

## Power management

- powertop: management tool
- tlp: configuration tool

## Clipboard managers

## Package management

## Remote Desktop Client

- Chrome Remote Desktop
- UltraVNC
- TightVNC
- Remmina (Linux only)
- TigerVNC
- Vinagre
- X2Go

### Non-open source

- Team Viewer
- AnyDesk
- NoMachine


## PDF Utilities

| Program               | Description                                     |
| -                     | -                                               |
| convert (ImageMagick) | Converting images to pdf(s) or pdf(s) to images |
| gs (ghostscript)      | Multiple functions                              |
| pdfunite (poppler)    | Merging pdfs                                    |
| pdfjam (texlive-core) | Merging pdfs                                    |
| pdfimages (poppler)   | Extracting images in pdfs                       |
| pdftk                 | Multiple functions                              |

- Compress pdfs
    + `gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf`
    + https://askubuntu.com/questions/113544/how-can-i-reduce-the-file-size-of-a-scanned-pdf-file
    + http://milan.kupcevic.net/ghostscript-ps-pdf/

```
-dPDFSETTINGS=/screen   (screen-view-only quality, 72 dpi images)
-dPDFSETTINGS=/ebook    (low quality, 150 dpi images)
-dPDFSETTINGS=/printer  (high quality, 300 dpi images)
-dPDFSETTINGS=/prepress (high quality, color preserving, 300 dpi imgs)
-dPDFSETTINGS=/default  (almost identical to /screen)
```

## Other

- [lostfiles](https://github.com/graysky2/lostfiles)
- [pkgtools](https://github.com/Daenyth/pkgtools)

# Documents and texts

## Office suite

[LibreOffice](https://www.libreoffice.org/)

## Documents markup languages

- [Markdown](http://daringfireball.net/projects/markdown)
- [asciidoc](http://asciidoc.org/): used by Arch for generating pacman's
  man pages
- [Pandoc](http://johnmacfarlane.net/pandoc): converting one markup file
  into another
- [txt2tags](https://en.wikipedia.org/wiki/Txt2tags)

## Scientific documents

- [TeX, LaTeX and friends](https://wiki.archlinux.org/index.php/TeX_Live)
- [TeXstudio](https://en.wikipedia.org/wiki/TeXstudio)
- [TeXmaker](https://en.wikipedia.org/wiki/Texmaker)
- [vim-latexsuite](https://wiki.archlinux.org/index.php/Vim)
- sublime with latextool or latexing plugin
- [Zotero](https://www.zotero.org/)

## Text editor

- [vi](https://wiki.archlinux.org/index.php/Vi)
- [vim](https://wiki.archlinux.org/index.php/Vim)
- [neovim](https://wiki.archlinux.org/index.php/Neovim)
- [gvim](https://wiki.archlinux.org/index.php/GVi)
- [emacs](https://wiki.archlinux.org/index.php/Emacs)
- sublime-text
- visual-studio-code
- atom

## Readers and Viewers

### E-book applications

- [Calibre](https://en.wikipedia.org/wiki/Calibre_(software))
- bookworm
- atril
- xreader
- mupdf

### PDF and DjVu

- [zathura](https://en.wikipedia.org/wiki/Zathura_(document_viewer))
- [apvlv](http://naihe2010.github.com/apvlv/): Lightweight PDF, DjVu,
  UMD, TXT viewer with Vim keybindings
- [evince](https://en.wikipedia.org/wiki/Evince)
- [Foxit Reader](https://aur.archlinux.org/packages/foxitreader/)

### [Terminal pagers](https://en.wikipedia.org/wiki/Terminal_pager)

- [less](https://wiki.archlinux.org/index.php/Core_utilities#less)
- [more](https://en.wikipedia.org/wiki/More_(command))
- [most](https://en.wikipedia.org/wiki/Most_(Unix))
- [vimpager](https://www.archlinux.org/packages/?name=vimpager)

### CHM

- [xchm](https://en.wikipedia.org/wiki/xCHM)

## Desktop Publishing

- [scribus](https://en.wikipedia.org/wiki/Scribus)

# Security

## Network security

Something

## Threat and vulnerability detection

Something

## File security

Something

## Anti malware

Something

## Backup programs

Something

## Screen lockers

Something

## Hash checkers

Something

## Encryption, signing, steganography

Something

## Password managers

- lastpass-cli
- bitwarden: https://bitwarden.com/
- pass: (zx2c4)
- gopass: new fork of pass written in go
    + https://news.ycombinator.com/item?id=13551692
    + https://www.justwatch.com/blog/post/announcing-gopass/
- seahorse: manage gnome-keyring

## Firewall management

Something

# Science

# Work environment

## Bootsplash

## Command shells

## Terminal multiplexers

## Desktop environment

- https://wiki.archlinux.org/index.php/Desktop_environment
- cinnamon
- enlightenment
- gnome
- lxde

## Window managers

### Stacking

- enlightenment
- openbox
- [tinywm](http://incise.org/tinywm.html)

### Tiling or Dynamic

- [i3](https://wiki.archlinux.org/index.php/I3)
- [dwm](https://wiki.archlinux.org/index.php/Dwm)
- [awesome](https://wiki.archlinux.org/index.php/Awesome)
- [xmonad](https://wiki.archlinux.org/index.php/Xmonad)

## Taskbars

- tint2

## Application luanchers

- dmenu
- rofi

## Window tilers

## Virtual desktop pagers

## Support applications

## Accessibility - Speech recognition

## Virtualization

- virtual box
- vmware

# Programming

## Languages

### Python

- [virtualenvwrapper](https://wiki.archlinux.org/index.php/Python/Virtual_environment)

## Code Quality

- sonarqube

## Databases

- HeidiSQL
- mysql-workbench

### SQLite

- sqlitebrowser

## Design

- dia
- yed

## Web Stack

- LAMP
- WAMP
- XAMPP

## Integrated Development Environment (IDE)

- Eclipse: Java
- Codeblocks: C++/C
- intellij-idea-community-version: Java, Kotlin
- liteide: Go

## Issue tracking systems

- Redmine
- Flyspray
- Bugzilla
- JIRA

# Security Tools

# Tips and Tricks

## Fun commands

- aafire
- espeak: text to speech

## ASCII arts

- ASCII text banners
    + toilet (aur)
    + figlet
    + banner
- images to ASCII
    + jp2a
- funny
    + cowsay
    + ponysay
    + asciiquarium
    + asciiportal (puzzle game)
- diagram
    + javE (aur)
    + asciio (aur)
    + vim-drawit (plugin)
    + http://asciiflow.com/
    + ditaa
- print logo
    + neofetch
    + screenfetch
