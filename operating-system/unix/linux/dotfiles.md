[TOC]

# Overview
In Unix-like operating systems, any file or folder that starts with a dot character (for example, `/home/user/.config`), commonly called a dot file or `dotfile`, is to be treated as hidden – that is, the `ls` command does not display them unless the `-a` flag (`ls -a`) is used.

The notion that filenames preceded by a `.` should be hidden in Unix was probably an unintended consequence of trying to make `ls` not show `.` and` ..`. [A lesson from shortcuts](https://plus.google.com/u/0/+RobPikeTheHuman/posts/R58WgWwN9jp)

A convention arose of using dotfile in the user's home directory to store per-user configuration or informational text. Dotfiles are used to customize your system with purpose is improving your productivity.

# Why use dotfiles with VCS (version control system)?
- Distributed backups: exploring new things without fear + restoring when disaster happen.
- History: improving yourself, debug
- Sharing: learn from each other + making life more meaningful
