[TOC]

# Overview

Mac OS

# Shortcuts - Key Binding

- Enter a directory: `Cmd + Down arrow`
- To the parent directory: `Cmd + Up arrow`
- To expand / collapse a directory: `Cmd + Right/Left arrow`
- Toggle showing hidden files in Finder: `Cmd + Shift + .`

## Swap / Remap keys using software

- Karabiner-Elements software can help with this.
- Typical remaps:
    + escape : grave_accent_and_tilde
    + caps_lock : escape
    + left_option : left_command (and vice versa)

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

## NAS (Network Attached Storage)

- How to connect the Finder to a NAS
    + `Go -> Connect to Server` or `Cmd+K`
    + In the server address bar, type your server address such as
        * `smb://192.168.50.213/data`
        * `smb://<server-domain-or-ip>/<folder-path>`
        * Click `+` sign to add the server to favorite list
    + Connect and enter credentials: user name and password

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

# Chrome / Chromium

- Bookmark manager: `Option + Cmd + b`
- Bookmark bar: `Shift + Cmd + b`
- Bookmark: `Cmd + d`
- Undo bookmark: `Cmd + d, Option + r`

# MacBook Air 13-inch 2017

- Latest macOS that support the machine is Monterey.
- macOS version history
    + 10.15: Catalina (2019)
    + 11: Big Sur (2020)
    + 12: Monterey (2021)
    + 13: Ventura (2022)
    + 14: Sonoma (2023)
    + 15: Sequoia (2024)

# Tips and Tricks

## Prevent sleeping when closing the lid

- https://apple.stackexchange.com/questions/219885/use-caffeinate-to-prevent-sleep-on-lid-close-on-battery
    + Run `noz` command

```sh
#!/bin/bash
#***************************************************************************
#*** noz - prevent laptop from sleeping when lid is closed
#***************************************************************************

#***** set some defaults *****
DEF_WAKE_LEN=900 # in seconds

#***** determine timeout value *****
timeout_len=${1:-$DEF_WAKE_LEN}

function prevent_sleep() {
    echo
    echo -n "Preventing sleep for $timeout_len seconds; press <enter> to continue..."
    sudo pmset -b disablesleep 1
}

function enable_sleep() {
    # $1: <enter> = 0, timeout = 1, Ctrl-C = undef

    #----- insert a newline for timeout or Ctrl-C -----
    if [[ ${1:-1} -eq 1 ]]; then    echo; fi

    sudo pmset -b disablesleep 0

    #----- sleep on timeout only -----
    if [[ ${1:--1} -eq 1 ]]; then   sudo pmset sleepnow; fi
    exit
}

#***** prevent it from sleeping *****
prevent_sleep

#***** trap Ctrl-C *****
trap enable_sleep INT

#***** wait for an enter *****
read -t $timeout_len
rc=$?

#***** re-enable normal sleep *****
enable_sleep $rc
```

## Configure memu bar (top of screen)

- Go to Settings, then Control Center

## Application Preferences are stored in

- `~/Library/Preferences`
    + `~/Library/Preferences/com.googlecode.iterm2.plist`

## Group files on Desktop

- Right click on the desktop
- Select `Use Stacks`

## Backup photos and images from phone to computer and external hard drives

- Connect phone to the computer.
- Using Finder app or Photos app or Image Capture app
    + Image Capture app can export / download photos directly from phone
      to external hard drives.
    + Finder app and Photos app we need to import to computer before
      copying to the external hard drives.

## Unzip multiple zip files to the same folder recursively

- Google Takeout zip files:
    + `ditto -x -k -V takeout-*.zip result 1>unzipped-log.txt 2>&1`

## Cron jobs

- https://apple.stackexchange.com/questions/402132/cronjobs-do-not-run
- Grant `cron` full disk access
    + Go to Security settings
    + Add `cron` to the list if it does not exist
    + `Cmd + Shift + G` to open the go to pop up with path
    + Type `/usr/sbin/cron`
- Debug the cron job
    + Touch a file every minute to see whether the cronjob works
    + Redirect error and output to a file

```
* * * * * /usr/bin/touch /Users/trnso/tmp/cronjob-success-"$(date)".txt
* * * * * /Users/trnso/Documents/repo/pri-scripts/amazon/refresh-aea-cookie-cron.sh >> /Users/trnso/tmp/cronjoblogs 2>&1
```


## Find processes that listen to a port and kill them

- https://pimylifeup.com/macos-kill-process-port
- Find processes that listen to a port
    + `sudo lsof -i tcp:<port>`

## Find all ports that are listening

- `sudo lsof -iTCP -sTCP:LISTEN -P`
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


# Troubleshooting

## zsh (qterm)(16532) MallocStackLogging: can't turn off malloc stack logging because it was not enabled

- The error message above is displayed in the terminal repeatedly when
  executing commands or in Vim editor.
- As of 20251015, this is caused by Amazon Q application (the UI app),
  turned it off fix the issue.
