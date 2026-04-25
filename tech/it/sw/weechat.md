[TOC]

# Overview

WeeChat is a fast, light and extensible chat client. It runs on many
platforms like Linux, Unix, BSD, GNU Hurd, Mac OS X and Windows
(bash/ubuntu and cygwin).

# Features

- Free software, multi-platform: Linux, FreeBSD, OpenBSD, NetBSD, Unix,
  GNU Hurd, Mac OS X, Windows (bash/ubuntu and cygwin)
- Light and extensible
    + A lightweight core
    + Optional plugins
    + Almost everything is a plugin
- Innovating features:
    + 256 colors
    + Mouse support
    + Customizable bars
    + 7 script languages
    + Horizontal/vertical split
    + Dynamic filtering of lines
    + Incremental text search
    + FIFO pipe
    + Spell checking
    + Scripts manager
    + Remote interfaces
    + Upgrade without quitting
- Full-featured IRC plugin
    + IRC plugin implements the protocol as described in the RFCs 1459
      and 2812.
    + Built-in features:
        * Multi-servers
        * IPv6, SSL, proxy
        * SASL authentication
        * Nicklist
        * Color for nicks
        * Color for away nicks
        * Smart filter
        * Anti-flood
        * Commands redirection
        * Custom CTCP replies
        * Lag indicator
        * DCC (file/chat)
- Remote interfaces
    + External interfaces (graphical or text) can connect to a running
      WeeChat.
    + Glowing Bear - HTML 5
    + QWeeChat - Qt interface
    + weechat-android
    + weechat.el - Emacs
    + weecloud - Javascript

# Quick Start

- https://weechat.org/files/doc/weechat/stable/weechat_quickstart.en.html
- FAQ:
    + https://weechat.org/files/doc/weechat/stable/weechat_faq.en.html

## Online Help

- `/help`
- `/help command`
- `/help config.section.option`

## Set options

- `/set config.section.option value`
    + WeeChat immediately uses the new value.
- To browser options and change them:
    + `/fset weechat.*`
    + `/fset irc.*`

## Core vs plugins

- WeeChat core is only used to display data on screen and interact with
  the user.
- All network protocols like IRC are provided in separate plugins.
- List loaded plugins:
    + `/plugin`

## Connecting to a server and channel

- Adding a new server:
    + Suport TLS: `/server add libera irc.libera.chat/6697 -tls`
    + Server does not support TLS:
        * `/server add <server_name> <domain>/<port>`
    + Server with password:
        * `/server add znc-libera 192.168.50.213/6697 -ssl -password=glider/libera:mypass`
- Set custom IRC server option before first time connecting.
- Connect to the server:
    + `/connect libera`
- More documentation
    + `/help server`
- Join a channel: `/join #channelname`
- Part a channel: `/part [quit message]`
- Close a server, channel or private buffer:
    + `/close`
- Disconnect from server: `/disconnect`

## Set custom IRC server options

- WeeChat uses default values for all servers if you don't specify a
  specific value for a server option.
    + `irc.server_default.*`
- For each server option, WeeChat uses its value if it is defined (not
  null)
- Common usage:
    + nicks:
        * `/set irc.server.libera.nicks "mynick,mynick2,mynick3,mynick4,mynick5"`
    + User and real names:
        * `/set irc.server.libera.username "My user name"`
        * `/set irc.server.libera.realname "My real name"`
    + Auto-connect to server at startup:
        * `/set irc.server.libera.autoconnect on`
    + SASL authentication to the server
        * `/set irc.server.libera.sasl_username "mynick"`
        * `/set irc.server.libera.sasl_password "xxxxx"`
    + To run a command after connecting to server, for example, to
      authenticate with NickServ (only if you don't user SASL for
      authentication):
        * `/set irc.server.libera.command "/msg nickserv identify xxxxxxx"`
    + To auto join some channels:
        * `/set irc.server.libera.autojoin "#channel1,#channel2"`
    + You can also configure WeeChat to automatically update the
      autojoin option when you join or leave channels:
        * `/set irc.server_default.autojoin_dynamic on`
    + Unset custom option:
        * `/unset irc.server.libera.nicks`

- If you want to protect your password in configuration files, you can use secured data.
    + First setup a passphrase:
        * `/secure passphrase this is my secret passphrase`
    + Then add a secured data with your libera password:
        * `/secure set libera_password xxxxxxx`
    + Then you can use `${sec.data.libera_password}` instead of your
      password in the IRC options mentioned above, for example:
        * `/set irc.server.libera.sasl_password "${sec.data.libera_password}"`

## IRC private messages

- Open a buffer and send a message to another user (nick foo):
    + `/query foo this is a message`
- Close the private buffer: `/close`

## Buffer/window management

- A buffer is a component linked to a plugin with a number, a category,
  and a name.
    + A buffer contains the data displayed on the screen.
- A window is a view on a buffer.
    + By default there is only one window displaying one buffer.
    + If you split the screen, you will see many windows with many
      buffers at the same time.
- Commands:
    + `/buffer`
    + `/window`
- Split window: `/window splitv 50`
- Remove the split: `/window merge`

## Key bindings

- Full documented:
    + https://weechat.org/files/doc/weechat/stable/weechat_user.en.html#key_bindings
- Important Keys:
    + `Alt + <arrow_left>/<arrow_right>` or `f5/f6`: switch to
      previous/next buffer
    + `f1/f2`: scroll bar wit hlist of buffers ("buflist")
    + `f7/f8`: switch to previous/next window (when screen is split)
    + `f9/f10`: scroll title bar
    + `f11/f12`: scroll nicklist
    + `Tab`: complete text in input bar
    + `PgUp/PgDn`: scroll text in current buffer
    + `Alt+a`: jump to buffer with activity (in hotlist)
- Rebind any key to a command with `/key` command:
    + To find key code: `Alt+k`.
    + For example to bind `Alt+!` to the command `/buffer close`:
        * `/key bind (press alt+k) (press alt+!) /buffer close`
    + To remove key: `/key unbind meta-!`

## Plugins / scripts

- Plugins might be available via a separate package.
    + Plugins are automatically loaded when found.
- External scripts can be downloaded and installed:
    + `/script install go.py`
    + `/help script` for more details

## Status bar meaning

- `[H: 3(1,8,2,4), 2(4)]`: a hotlist, a list of buffers with the number
  of unread messages
    + Buffer 3 has: 1 highlight (magenta), 8 private messages (green), 2
      messages (yellow/brown), 4 other messages (default color of text
      in terminal) (join/part messages)
- Colors can be change through options: `weechat.color.status_data_*`
  (buffers) and `wechat.color.status_count_*` (counters)

## Mouse

- Enable mouse support: `/mouse enable`
- Usage:
    + Scrolling
    + Left click
        * and swipe to move to the next/previous buffer.
        * nick to create private chat buffer with that nick
    + Right click
        * to join the channel
        * to whois a nick
    + Hold `Shift` to select text

## Common IRC commands

- `/whois [<server>] <nicknames>`
    + Returns info about the comma-separated list of nicknames masks.
- `/who [<name> ["o"]]`
    + Return a list of users who match the name.
    + if the flag "o" is given, only return info about IRC operators.

## Upgrading

- WeeChat can be upgraded without disconnecting from the IRC servers
  (plaintext connections only, not TLS)
    * `/upgrade`: load the new WeeChat binary and reload the current
      configuration.

# User Guide

- https://weechat.org/files/doc/weechat/stable/weechat_user.en.html

## Interface

## Key bindings

### Command Line

### Buffers

- `Ctrl+r`: search for text in command history.
    + `/input search_history`
- `Ctrl+s`: search for text in buffer lines.
    + `/input search_text_here`
- `Ctrl+x`: switch current buffer if buffers are merged with same
  number, for example switch to another IRC server buffer.
    + `/buffer switch`
- `Alt+x`: zoom on a merged buffer (`Alt+x` again to display all merged
  buffers)
    + `/buffer zoom`
- Scrolling:
    + `PgUp`: up one page
        * `/window page_up`
    + `PgDn`: down one page
        * `/window page_down`
    + `Alt+PgUp`: up a few lines
        * `/window scroll_up`
    + `Alt+PgDn`: down a few lines
        * `/window scroll_down`
    + `Alt+Home`: to the top of buffer
        * `/window scroll_top`
    + `Alt+End`: to the bottom of buffer
        * `/window scroll_bottom`

### Search Text Context

- These keys are used in context "search" (when `Ctrl+s` is pressed to
  search text in buffer lines)
- `Ctrl+x`: switch search type: string (default), regular expression
    + `/input search_switch_regex`
- `Alt+c`: switch exact case for search
    + `/input search_switch_case`
- `Ctrl+r` or `<arror_up>`: previous occurrence
    + `/input search_previous`
- `Ctrl+s` or `<arrow_down>`: next occurrence
    + `/input search_next`
- `Enter` or `Ctrl+j` or `Ctrl+m`: stop search at current position
    + `/input search_stop_here`
- `Ctrl+q`:  stop search and reset scroll to pre-text search state
    + `/input search_stop`

### Search Command History Context

- These keys are used in context "histsearch" (when `Ctrl+r` is pressed to
  search text in command history)
- `Ctrl+x`: switch search type: string (default), regular expression
    + `/input search_switch_regex`
- `Alt+c`: switch exact case for search
    + `/input search_switch_case`
- `Ctrl+r` or `<arror_up>`: previous occurrence
    + `/input search_previous`
- `Ctrl+s` or `<arrow_down>`: next occurrence
    + `/input search_next`
- `Enter` or `Ctrl+j` or `Ctrl+m`: stop search at current position
    + `/input search_stop_here`
- `Ctrl+q`:  stop search and restore input to its initial  value
    + `/input search_stop`

## Configuration

- To store all configuration files in a single directory:
    + Set `WEECHAT_HOME` environment.
    + `export WEECHAT_HOME=~/.config/weechat`
- By default WeeChat stores its configuration files in XDG directories.
    + Editing these files directly is not recommended.
    + Instead you should use the `/set` command.
        * https://weechat.org/files/doc/devel/weechat_user.en.html#command_weechat_set
    + To get a list of all configurable options run `/set` in the
      WeeChat buffer window.
    + Search options: `/set irc.server.*` or `/set *server*`
    + Can get help on each option: `/help irc.server.libera.autoconnect`


## IRC

### Custom CTCP Replies

- https://weechat.org/files/doc/weechat/stable/weechat_user.en.html#irc_ctcp_replies

## Xfer

- `Xfer` plugin brings:
    + direct chat (between 2 hosts, without server)
    + file transfer

## Typing notifications

## External Commands

- `/exec` command lets you execute external commands inside WeeChat and
  display output locally, or send it to a buffer.

## FIFO pipe

- You can remote control WeeChat, by sending commands or text to a FIFO
  pipe (if option `fifo.file.enabled` is set, it is by default)

## Trigger

- Trigger is the Swiss Army knife for WeeChat: it can hook many things
  (signal, modifier, print, etc.), change the content of data, and
  execute one or more commands.

## Extending WeeChat

### Plugins

### Scripts

# Archlinux

## Spell Check

- Install spell check backend:
    + `sudo pacman -S enchant aspell-en`
- Load the new plugin in WeeChat if it's not loaded
    + `/plugin load spell`
- Set default dictionary:
    + `/set spell.check.default_dict "en"`
- Enable spell checking:
    + `/set spell.check.enabled on`
- Display corrections:
    + `/set spell.check.suggestions 3`
- Add suggestions to status bar:
    + `/set weechat.bar.status.items "[buffer_count],[buffer_plugin],buffer_number+:+buffer_name+(buffer_modes)+{buffer_nicklist_count}+indent,spell_suggest,hotlist"`

# References

[weechat]: https://wiki.archlinux.org/index.php/WeeChat "Arch Wiki - Weechat"
[homepage]: https://weechat.org/ "Weecha"

