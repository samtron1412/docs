[TOC]

# Overview

Mac OS

# Tuning Mac

- https://github.com/nikitavoloboev/my-mac-os
- https://github.com/serhii-londar/open-source-mac-os-apps
- https://github.com/iCHAIT/awesome-macOS
- https://github.com/jaywcjlove/awesome-mac

# Application and Work flows

## Productivity

- Alfred/Quicksilver: launcher
- Karabiner: keyboard remapping
- Keyboard Maestro: automation tool
    + [Hammerspoon](http://www.hammerspoon.org/)
- emacs org-mode: todo list and task management
- Google Calendar: notes (Google Keep), todo list (Google Tasks)
- docs, pri-doc, etc.: project management, Trello alternative
- lastpass
- Dictionary (built-in)
- [Focus](https://heyfocus.com/): block distracting websites
- [Timing](https://timingapp.com/?): time tracker
- PDF Expert + PDF Foxit reader
- sVim (github): vim-like safari extension
- hugo: the fastest way to build a static website
- speedtest-cli
- fkill: an alternative for kill, can search, interactive UI
    + Install: `npm install --global fkill-cli`
- yarn: nodejs package manager
- nvm: node version manager
- jenv: java version manager

## Command-line tools

- fzf: command-line fuzzy finder
- ripgrep: search text for patterns
- fd: a simple alternative for find
- exa: an alternative for ls
- bat: an alternative for cat
- m-cli: manage macOS administrative tasks
- diskutil: built-in macOS command line (similar lsblk)
- pbcopy, pbpaste: built-in macOS command line (copy and paste to
  Clipboard)


## Game

- Battle for Wesnoth
- Chess (built in)
- OpenEmu: NES, SNES, etc. (Mario, Bloody Roar, etc.)
- A Slower Speed of Light

# Java

- https://stackoverflow.com/questions/26252591/mac-os-x-and-multiple-java-versions
- brew install java: current java version
- brew install java11

# Tips and Tricks

## Reinstall Xcode developer tools

`xcode-select --install`

## Replace the old hard disk with a new one

- Boot to the Recovery Mode by Restart and holding down Command+R
    + Start Disk Utility and delete any volumes on the new disk and
      erase the disk, format the disk using appropriate file systems
        * APFS: the newest file system
        * HFS: the old file system since 1998
    + When erase the disk using GUID partition scheme
- Quit Disk Utility and Reinstall the macOS on the new hard disk
    + During the installation, choose transferring data from the old
      disk to the new disk

## Key repeat

- Hold a key and it will repeat the key in Sublime Text in vim mode
- https://gist.github.com/conficker1805/18830beb333a990b22a3
- Enable key repeat for an app:
    + `defaults write com.sublimetext.3 ApplePressAndHoldEnabled -bool false`
- Enable key repeat for the whole system:
    + `defaults write -g ApplePressAndHoldEnabled -bool false`
- Disable key repeat for the whole system:
    + `defaults write -g ApplePressAndHoldEnabled -bool true`
- Restart app after changing the setting


```
You can disable this feature for just Sublime Text by issuing the
following command in your terminal (not the Sublime Text console):

defaults write com.sublimetext.3 ApplePressAndHoldEnabled -bool false

Note: replace com.sublimetext.3 with whichever version of Sublime Text
you are running eg. 'com.sublimetext.2'

Alternately, if you want this feature disabled globally, you can enter
this:

defaults write -g ApplePressAndHoldEnabled -bool false

In either case you'll need to restart Sublime Text for the change to
take place.
```

## Create a Python development environment

- https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-macos
- https://hackercodex.com/guide/python-development-environment-on-mac-osx/
- install homebrew
- install python through brew install python
- install virtualenv through pip install virtualenv
