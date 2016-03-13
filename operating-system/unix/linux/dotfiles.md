[TOC]

# Overview
In Unix-like operating systems, any file or folder that starts with a dot character (for example, `/home/user/.config`), commonly called a dot file or `dotfile`, is to be treated as hidden – that is, the `ls` command does not display them unless the `-a` flag (`ls -a`) is used.

The notion that filenames preceded by a `.` should be hidden in Unix was probably an unintended consequence of trying to make `ls` not show `.` and` ..`. [A lesson from shortcuts](https://plus.google.com/u/0/+RobPikeTheHuman/posts/R58WgWwN9jp)

A convention arose of using dotfile in the user's home directory to store per-user configuration or informational text. Dotfiles are used to customize your system with purpose is improving your productivity.

# Why use dotfiles with VCS (version control system)?
- Distributed backups: exploring new things without fear + restoring when disaster happen.
- History: improving yourself, debug
- Sharing: learn from each other + making life more meaningful

# How can we manage the dotfiles?
- Most likely, as a developer, you will keep using and improving your dotfiles for your entire career. Your dotfiles will most likely be the *longest project you ever work on*. For this reason, it is worthwhile to organize your dotfiles project in a disciplined manner for **maintainability** and **extensibility**.

## Organizational Approaches
- Having your entire home directory under VCS (and ignore/exclude files which you don't want to commit)
- Keeping your configuaration files in a seperate directory and symlink them into place. This approache is vastly superior for sevveral reasons:
	+ There is no possibility of accidentally deleting your files. With your entire home directory under VCS, running something like a `git clean` could wipe out everything in your home directory that is not tracked by your VCS.
	+ It is possible to track configuration files that belong somewhere other than `$HOME`.
	+ Installing dotfiles on new machines is easier. All that is required is cloning your dotfiles followed by linking files. Keepping the entire home directory under VCS complicates installation.
