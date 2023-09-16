[TOC]

# Overview

Mac OS

# Shortcuts - Key Binding

- Enter a directory: `Cmd + Down arrow`
- To the parent directory: `Cmd + Up arrow`
- To expand / collapse a directory: `Cmd + Right/Left arrow`

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

- Install any Java version that you want, and then using the following
  aliases to set Java version on the fly.

```
# JAVA LANGUAGE RUNTIMES
export JAVA_8_HOME=/Library/Java/JavaVirtualMachines/amazon-corretto-8.jdk/Contents/Home
export JAVA_11_HOME=/Library/Java/JavaVirtualMachines/amazon-corretto-11.jdk/Contents/Home
alias java8='export JAVA_HOME=$JAVA_8_HOME'
alias java11='export JAVA_HOME=$JAVA_11_HOME'
alias nojava='unset JAVA_HOME'

# default to Java 11
java11
```

# Mail.App

## Shortcuts

- Show hidden files: `cmd + shift + .`
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

## Find all ports that are listening

- `sudo lsof -iTCP -sTCP:LISTEN -P | grep ssh`

## Listing all DNS server that are configured

- `scutil --dns | grep nameserver | sort -u`

## Write to (and read from) NTFS file system

- https://techsviewer.com/how-to-write-ntfs-drives-on-macos-monterey/
- It looks like it only work for Monterey
- Create a new directory to mount the disk with write options.

```
# List all disks to identify the identifier of the disk
Diskutil list

# Replace `disk2s1` with the identifier of the NTFS disk
Sudo mkdir /Volumes/disk2s1

# Mount the disk with read write options
Sudo mount -t ntfs -o rw,auto,nobrowse /dev/disk2s1 /Volumes/disk2s1
```

## Ensure all traffic is going through the proxy

- tun2socks
    + https://github.com/xjasonlyu/tun2socks
- sshuttle
    + https://github.com/apenwarr/sshuttle
    + http://teohm.com/blog/using-sshuttle-in-daily-work/
- https://superuser.com/a/803010/280467
    + Using `ipfw` for macOS instead of `iptables`

## Install pygraphviz

- https://stackoverflow.com/questions/32933480/error-while-installing-pygraphviz-mac-os-x-anaconda
- `brew install graphviz`
- `pip install --global-option=build_ext --global-option="-IC:/usr/local/include/" --global-option="-LC:/usr/local/lib/" pygraphviz`

## If the Software Update hanging (keep checking)

- Run this command: `sudo /bin/launchctl kickstart -k system/com.apple.softwareupdated`

## Xprotect is not recent

- https://community.jamf.com/t5/jamf-pro/force-xprotect-to-update/m-p/225543
- Go to Software Update and check
    + `Check for updates`
    + `Download new updates when available`
    + `Install system data files and security updates`
- Run `softwareupdate --background --include-config`

## Record System/Internal Audio with Mic Audio

- Install Blackhole using brew
    + https://github.com/ExistentialAudio/BlackHole
- Add a multi-ouput device
    + https://github.com/ExistentialAudio/BlackHole/wiki/Multi-Output-Device
    + Open MIDI
    + Output: blackhole + external headphones
    + Master: headphones
    + Drift correction: blackhole
    + Right-click and select: `Use this device for sound OUTPUT`
- Add an aggregate device
    + Open MIDI
    + Input: blackhole + mic
    + Output: blackhole
    + Clock source: mic
    + Drift correction: blackhole
    + Right-click and select: `Use this device for sound INPUT`
- Open QuickTime Player to record audio
    + Select the input is the created aggregate device

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

