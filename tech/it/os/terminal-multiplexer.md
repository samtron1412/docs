[TOC]

# Overview
A terminal multiplexer is a software application that can be used to multiplex several virtual consoles, allowing a user to access multiple separate login sessions inside a single terminal window or detach and reattach session from a terminal. It is useful for dealing with multiple programs from a command line interface, and for separating programs from the session of the Unix shell that started the program. Particularly so a remote process continues running even when the user is disconnected.

# Features
A terminal multiplexer can be thought of as a text version of window managers, or as a way of putting attach virtual terminals to any login session.

It is a wrapper that allows multiple text programs to run at the same time, and provides features that allow the user to use the programs within a single interface productivity.

## Persistence
- A terminal multiplexer allows the user to start applications from one computer, and then reconnect from a different computer and continue using the same application without having to restart it. This makes accessing the same session between different locations like work and home simple.
- The multiplexer starts a session and this session can detach (for example if the network connection is dropped). Since the session does not end, the processes are not sent a "hangup" signal ([SIGHUP][2]) and are not terminated.

## Multiple windows
- Multiple terminal sessions can be created, each of which usually runs a single application.
- The windows are numbered, each window has its own scroll-back buffer.
- Windows can be split-screened.

## Session Sharing
- Allow multiple computers to connect to the same session at once.
- Enabling collaboration between multiple users.
- The same computer can also be used to make multiple simultaneous connections, providing alternative functionality to screen-splitting, particularly for computers with multiple monitors.

# Implementations
- [GNU Screen](https://en.wikipedia.org/wiki/GNU_Screen)
- [tmux](https://en.wikipedia.org/wiki/Tmux)
- [Byobu](https://en.wikipedia.org/wiki/Byobu_(software))

# References
1. [Terminal Multiplexer - Wikipedia][1]

[1]: https://en.wikipedia.org/wiki/Terminal_multiplexer "Terminal Multiplexer - Wikipedia"
[2]: https://en.wikipedia.org/wiki/SIGHUP "SIGHUP - Wikipedia"
