[TOC]

# Overview
- [Homepage](http://www.zsh.org/)
- [wikipedia](https://en.wikipedia.org/wiki/Z_shell)
- [Awesome list for ZSH](https://github.com/unixorn/awesome-zsh-plugins)

The Z shell (zsh) is a **Unix shell**. Zsh can be thought of as an extended Bourne shell with a large number of improvements, including some features of bash, ksh, and tcsh. It offers many advantages such as:
- Efficiency
- Improved tab completion
- Improved globbing (specify sets of filename with wildcard characters)
- Improved array handling
- Full customisability

**Paul Falstad** wrote the first version of zsh in 1990 while a student at Princeton University

# Configuration files
When starting Zsh, it'll source the following files in this order by default:

`/etc/zsh/zshenv`: **NO**
This file should contain commands to set the global command search path and other system-wide environment variables; it should not contain commands that produce output or assume the shell is attached to a tty.

`~/.zshenv`: **NO**
Similar to /etc/zsh/zshenv but for per-user configuration. Generally used for setting some useful environment variables.

`/etc/zsh/zprofile`: **USE BUT NO MODIFY**
This is a global configuration file, it'll be sourced at login. Usually used for executing some general commands at login. Please note that on Arch Linux, by default it contains one line which source the `/etc/profile`.

`/etc/profile`: **USE BUT NO MODIFY**
This file should be sourced by all Bourne-compatible shells upon login: it sets up an environment upon login and application-specific (`/etc/profile.d/*.sh`) settings. Note that on Arch Linux, Zsh will also source this by default.

`~/.zprofile`: **NO**
This file is generally used for automatic execution of user's scripts at login.

`/etc/zsh/zshrc`: **NO**
Global configuration file, will be sourced when starting as a interactive shell.

`~/.zshrc`: **YES - MAIN CONFIGURATION**
Main user configuration file, will be sourced when starting as a interactive shell.

`/etc/zsh/zlogin`: **NO**
A global configuration file, will be sourced at the ending of initial progress when starting as a login shell.

`~/.zlogin`: **NO**
Same as /etc/zsh/zlogin but for per-user configuration.

`/etc/zsh/zlogout`: **NO**
A global configuration file, will be sourced when a login shell exits.

`~/.zlogout`: **NO**
Same as /etc/zsh/zlogout but for per-user configuration.

>**Note**:
- The paths used in Arch's zsh package are different from the default ones used in the man pages
- `/etc/profile` is not a part of the regular list of startup files run for Zsh, but is sourced from `/etc/zsh/zprofile` in the zsh package. Users should take note that `/etc/profile` sets the **$PATH** variable which will overwrite any **$PATH** variable set in `~/.zshenv`. To prevent this, please set the **$PATH** variable in `~/.zprofile`

>**Warning**: It is not recommended to replace the default one line in `/etc/zsh/zprofile` with something other, it'll break the integrality of other packages which provide some scripts in `/etc/profile.d`

# Configuring ZSH
## Configure environment variables
- `$PATH`
- `$EDITOR`
- `$GIT_EDITOR`
- `$SAVEHIST`
- `$LSCOLORS`
- `$LS_COLORS`
- `$GPG_TTY`
- `$GPG_AGENT_INFO`

# Plugins manager
## [oh-my-zsh](http://ohmyz.sh/)
`lib`: contain many useful library for zsh. Read code to understand the details.
- Add environment variables
- Completion, git branches, correction, etc.

## [antigen](https://github.com/zsh-users/antigen)

## [zgen](https://github.com/tarjoilija/zgen)

# Plugins
## git

## [z](https://github.com/rupa/z)

## vi-mode

## history-substring-search

## sudo

## sublime

## tmux

## tmuxinator

## prompt
### robbyrussell

# Uninstallation

