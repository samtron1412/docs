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

# References
1. [GNU Screen - Wikipedia][1]
2. [GNU Screen source code - Git][2]

[1]: https://en.wikipedia.org/wiki/GNU_Screen "GNU Screen - Wikipedia"
[2]: http://git.savannah.gnu.org/cgit/screen.git/ "GNU Screen source code - Git"
