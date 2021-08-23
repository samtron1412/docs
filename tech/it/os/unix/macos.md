[TOC]

# Overview

Mac OS

# Tuning Mac

- https://github.com/nikitavoloboev/my-mac-os
- https://github.com/serhii-londar/open-source-mac-os-apps
- https://github.com/iCHAIT/awesome-macOS
- https://github.com/jaywcjlove/awesome-mac

# Application and Work flows

## Graphical Apps

- emacs org-mode: todo list and task management
- Google Calendar
- Google Keep
- Dictionary (built-in)
- PDF Expert + PDF Foxit reader
- Chess (built in)
- OpenEmu: NES, SNES, etc. (Mario, Bloody Roar, etc.)
- keka: file archiver

## Command-line tools

- speedtest-cli
- fkill: an alternative for kill, can search, interactive UI
    + Install: `npm install --global fkill-cli`
- JavaScript
    - nodejs: nodeJS
    - npm: nodejs package manager
    - yarn: nodejs package manager
- Search tools
    + fzf: command-line fuzzy finder
    + ripgrep (rg): search text for patterns
    + the_silver_searcher (ag): search tool similar ripgrep
    + fd: a simple alternative for find
- bat: an alternative for cat, less
- diskutil: built-in macOS command line (similar lsblk)
- pbcopy, pbpaste: built-in macOS command line (copy and paste to
  Clipboard)
- p7zip: file archiver



# Java

- https://stackoverflow.com/questions/26252591/mac-os-x-and-multiple-java-versions
- brew install java: current java version
- brew install java11

# Mail.App

## Shortcuts

- Preferences: `cmd + ,`
- New Message: `cmd + n`
- Undo: `cmd + u`
- Redo: `shift + cmd + u`
- Select all: `cmd + a`
- Paste as quotation: `shift + cmd + v`
- Get all new mails: `shift + cmd + n`
- Reply: `cmd + r`
- Reply all: `shift + cmd + r`
- Flag as read: `shift + cmd + l`
- Archive: `ctrl + cmd + a`
- Search mailbox: `alt + cmd + f`
- Search inside a mail: `cmd + f`

# Tips and Tricks

## Kill all WindowServer to restart the Window Manager

Sometimes, if you have problems with window manager / displays, and you
don't want to restart your computer, then you can kill all the window
servers to restart them.

- `sudo killall -1 WindowServer` or `sudo killall -HUP WindowServer`

## Places to check when cleaning storage

- StackOverflow
    + https://apple.stackexchange.com/questions/261252/system-storage-on-macos-sierra-is-470gb
- Using OmniDiskSweeper
    + https://www.omnigroup.com/more
- Using Grandperspective
    + http://grandperspectiv.sourceforge.net/
- https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/MacOSXDirectories/MacOSXDirectories.html
- `~/Documents`
- `~/Downloads`
- `~/Library/Application Support`
- `~/Library/Containers`
- `~/Library/Messages`
- `~/Library/Mail`
- `~/Music`
- `~/repo`

## Reinstall Xcode developer tools

`xcode-select --install`

## Replace the old hard disk with a new one with different sizes

- Since it is different in size, we cannot use the same method of
  cloning using Disk Utility
- Boot to the Recovery Mode by Restart and holding down Command+R
    + Start Disk Utility and delete any volumes on the new disk and
      erase the disk, format the disk using appropriate file systems
        * APFS: the newest file system
        * HFS: the old file system since 1998
    + When erase the disk using GUID partition scheme
- Quit Disk Utility and Reinstall the macOS on the new hard disk
    + During the installation, choose transferring data from the old
      disk to the new disk
- Install Xcode command tools: (for brew)
    + `xcode-select --install`

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

USING CONDA

## Cannot turn off Do not disturb

- `killall NotificationCenter`

