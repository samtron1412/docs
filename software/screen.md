[TOC]

# Overview
GNU Screen is a terminal multiplexer. Released under the terms of version 3 or later of the GNU General Public License.

# Features
- Such as a terminal multiplexer, GNU Screen has following features: persistence, multiple windows, and session sharing.
- GNU Screen is often used when a network connection to the terminal is unreliable, as a dropped network connection typically terminates all programs the user was running (child processes of the login session), due to the session ending and sending a "hangup" signal (SIGHUP) to all the child processes. Running the applications under GNU Screen means that the session does not terminate - only the now-defunct terminal gets detaches - so applications don't even know the terminal has detached, and allows the user to reattach the session later and continue working from where they left off.

# References
1. [GNU Screen - Wikipedia][1]

[1]: https://en.wikipedia.org/wiki/GNU_Screen "GNU Screen - Wikipedia"
