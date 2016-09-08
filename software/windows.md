[TOC]

# Overview

# Knowledge
## `AppData` folder each user
The AppData folder contains **app settings, files, and data specific** to the apps on your PC. The folder is hidden by default in File Explorer, and has three hidden sub-folders: `Local`, `LocalLow`, and `Roaming`.

`Roaming`. This folder (**%appdata%**) contains data that can move with your user profile from PC to PC—like when you're on a domain - because this data has the ability to sync with a server. For example, if you sign in to a different PC on a domain, your web browser favorites or bookmarks will be available.

`Local`. This folder (**%localappdata%**) contains data that can't move with your user profile. This data is typically specific to a PC or too large to sync with a server. For example, web browsers usually store their temporary files here.

`LocalLow`. This folder (**%appdata%/.../locallow**) contains data that can't move, but also has a lower level of access. For example, if you're running a web browser in a protected or safe mode, the app will only be able access data from the LocalLow folder.

The apps themselves choose whether to save to the Local, LocalLow, or Roaming folders. Most desktop apps use the Roaming folder by default, while most Windows Store apps use the Local folder by default.


# Tips and Tricks
## Big AppData
- Check Apple backup (iPhone, iPad, etc)

## Shortcut
### Move windows
These are the killer shortcuts for manipulating the active window:

- Win+Left arrow: Snap to the left half of the screen
- Win+RIght arrow: Snap to the right half of the screen
- Win+Up arrow: Maximize the window
- Win+Down arrow: Minimize/Restore if it's maximized

If you have more than one monitor:

- Win+Shift+Left arrow: Move window to the monitor on the left
- Win+Shift+Right arrow: Move window to the monitor on the right

## Turn off Hibernate
Run cmd at administrator and type command: `powercfg.exe /hibernate off`

## Delete the "nul" files
Open command prompt with administration permission and use this command: `Del \\?\C:\My\Path\NUL`

# Windows Keys
## Windows 10
### Pro
TY4CG-JDJH7-VJ2WF-DY4X9-HCFC6
VK7JG-NPHTM-C97JM-9MPGT-3V66T

### Education
VW6N7-Q9Q88-73MKM-GM9PR-F6YMY

# Office Keys
## Office 2013 Plus (Office 15)
YC7DK-G2NP3-2QQC3-J6H88-GVGXT

# Troubleshoot
## Block port
Run `Windows + R`: type `resmon.exe` => resources monitor windows.

## DNS_PROBE_*
Some similar errors: `DNS_PROBE_FINISHED_NO_INTERNET`, `DNS_PROBE_FINISHED_BAD_CONFIG`, `...`

Disabled `6to4` and `isatap` adapter: (these adapter use for transfer packets IPv6 under IPv4 network)
- `netsh int ipv6 isatap set state disabled`
- `netsh int ipv6 6to4 set state disabled`
- `netsh interface teredo set state disable`
- `netsh interface isatap set state disable`

0. Command line

		ipconfig /release
		ipconfig /renew
		ipconfig /flushdns
		netsh winsock reset

	After that restart computer.

1. Try [reset TCP/IP](https://support.microsoft.com/kb/299357?wa=wsignin1.0)

2. Reinstall adapter

	a. Go to Device Manager and expand Network adapter categories
	b. Right click the item stating wireless connection and choose to Uninstall
	c. Restart the computer
	d. After a restart the system will automatically install the driver
	e. However if it doesn’t then go back to Device Manager
	f. Right click username on the top of the list and choose to scan for hardware changes
	g. The system shall automatically recognize the missing drivers
	h. Following the instructions on Driver Software Installation wizard to set up network adapter
	i. Restart the computer once again and see if it works

3. Reinstall driver: Install the network drivers from the manufacturer website.

# [Windows Subsytem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)
A team of sharp developers at Microsoft has been hard at work adapting some Microsoft research technology to basically perform real time translation of **Linux syscalls** into **Windows OS syscalls**. Linux geeks can think of it sort of the inverse of "**WINE**" -- Ubuntu binaries running natively in Windows. Microsoft calls it a "Windows Subsystem for Linux

- [Linux test](https://github.com/linux-test-project/ltp)
