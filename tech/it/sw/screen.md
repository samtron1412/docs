[TOC]

# Overview
GNU Screen is a terminal multiplexer. Released under the terms of version 3 or later of the GNU General Public License.
## History
- Screen was originally designed by Oliver Laumann and Carsten Bormann and published in 1987.
- Around 1990, Laumann handed over maintenance of the code to Jürgen Weigert and Michael Schroeder.
- By 2014, Amadeusz Sławiński became maintainer.

# Terminology
- session: A single collection of windows - all running under a master screen process. The session can be given a name (e.g. myshells). Screen sessions each have their own clipboard, so copy and paste using the session's clipboard works exclusively between windows within that session.
- window: by default, windows are created with a shell running in them. Each window has a number unique within that session. It also has a name, which does not have to be unique.
- region: A portion of the display where a screen window is visible. The display can be split into multiple regions, so you can see multiple windows at once.
- display: This refers to where the screen session is attached; if being specific, it refers to the terminal or pseudo-terminal used by the attaching process.
- display terminal: The terminal to which screen is attached. Often an xterm or console window, but could be any terminal either physical or software. It is possible to have multiple displays terminals viewing the same screen session at the same time.
- virtual terminal: The terminal that screen windows provide to the programs running within them.

# Features
- Such as a terminal multiplexer, GNU Screen has following features: persistence, multiple windows, and session sharing.
	+ GNU Screen can multiplex a terminal. Within a single session, you can have multiple windows, each one behaving like a separate terminal. You can open email client in one window and text editor in another and be able to flip between them.
	+ GNU Screen support multiple attaching. You can attach to the same session from different terminals.
	+ GNU Screen keeps scroll back buffers for all of its windows. Each window has a separate buffer.
	+ GNU Screen is friendly with various charsets, including UTF-8.
	+ GNU Screen can lock its sessions when you're not using them.
	+ GNU Screen has (optional) multiuser support. You can have different people on the same computer all attached to the same session and watching each other's work.
	+ GNU Screen can split its display.
- GNU Screen is often used when a network connection to the terminal is unreliable, as a dropped network connection typically terminates all programs the user was running (child processes of the login session), due to the session ending and sending a "hangup" signal (SIGHUP) to all the child processes. Running the applications under GNU Screen means that the session does not terminate - only the now-defunct terminal gets detaches - so applications don't even know the terminal has detached, and allows the user to reattach the session later and continue working from where they left off.

# Usage
Commands are entered pressing the **escape key** `ctrl+a` and then the key binding.

## Common commands
- `ctrl+a ?`: Displays commands and its defaults
- `ctrl+a :`: Enter to the command prompt of screen
- `ctrl+a "`: Window list

### Getting out
- `ctrl+a d` Detach from the current screen session, and leave it running. Use `screen -r` to resume

### Window management
- `ctrl+a 0`: Opens windows 0
- `ctrl+a A`: Rename the current window
- `ctrl+a a`: Sends `ctrl+a` to the current window
- `ctrl+a c` Create a new window (with shell)

### Split screen
- `ctrl+a S` Split current region into two regions
- `ctrl+a tab` Switch the input focus to the next region
- `ctrl+a ctrl+a` Toggle between current and previous region
- `ctrl+a X` Close the current region
- `ctrl+a Q` Close all regions but the current one

### Misc
- `ctrl+a Esc` Enter Copy Mode (use enter to select a range of text)
- `ctrl+a ]` Paste text

## Command Prompt Commands
- `ctrl+a :quit`: closes all windows and sessions
- `ctrl+a :source ~/.screenrc`: reloads screenrc configuration file

## Named sessions
- Create a new named session: `$ screen -S session_name`
- Rename an existing session: `ctrl+a :sessionname session_name`
- Print a list of `pid.tty.host` string identifying your screen sessions: `$ screen -list` or `$ screen -ls`
- Attach to a named screen session: `$ screen -x session_name` or `$ screen -r session_name`
	+ The ultimate attach: `$ screen -dRR` (Attaches to a screen session. If the session is attached elsewhere, detaches that other display. If no session exists, creates one. If multiple sessions exist, uses the first one.)
- Detach a running session: `$ screen -d <name>`

## Autostart processes running inside screen with systemd
This service autostarts screen for the specified user (e.g. `systemctl enable screen@florian`). Running this as a system unit is important, because `systemd --user` instance is not guaranteed to be running and will be killed when the last session for given user is closed.

For example: `/etc/systemd/system/screen@.service`

```shell
[Unit]
Description=screen
After=network.target

[Service]
Type=simple
User=%i
ExecStart=/usr/bin/screen -DmS autoscreen
ExecStop=/usr/bin/screen -S autoscreen -X quit

[Install]
WantedBy=multi-user.target
```

# Tips and Tricks
## Use 256 colors
By default, screen uses an 8-color terminal emulator.

`~/.screenrc`

```
term rxvt-unicode-256color
```

## Informative statusbar
```
hardstatus off
hardstatus alwayslastline
hardstatus string '%{= kW} %= %H | %n | %f%t%?(%u)%? | %m-%d | %c %='
```

## Turn off welcome message
```
startup_message off
```

## Use X scrolling mechanism
```
termcapinfo rxvt* ti@:te@
```

## Nested Screen Sessions
It is possible to get stuck in a nested screen session. A common scenario: you start an ssh session from within a screen session. Within the ssh session, you start screen. By default, the outer screen session that was launched first responds to `ctrl+a` commands. To send a command to the inner screen session, use `ctrl+a a`, followed by your command.
- `ctrl+a a d`: detaches the inner screen session.
- `ctrl+a a K`: kills the inner screen session.

## Pull a process into screen
- [reptyr][3]
- Get the PID of the process. Type this command inside a screen window: `$ reptyr <pid>`

# References
1. [GNU Screen - Wikipedia][1]
2. [GNU Screen source code - Git][2]
3. [reptyr][3]

[1]: https://en.wikipedia.org/wiki/GNU_Screen "GNU Screen - Wikipedia"
[2]: http://git.savannah.gnu.org/cgit/screen.git/ "GNU Screen source code - Git"
[3]: https://github.com/nelhage/reptyr "reptyr"
