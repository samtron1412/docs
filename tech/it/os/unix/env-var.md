[TOC]

# Overview

An environment variable is a named object that contains data used by one
or more applications.
- It is a variable with a name and a value.
- Environment variables provide a simple way to share configuration
  settings between multiple applications and processes in Linux.
- They were introduced in their modern form in 1979 with Version 7 Unix,
  so are included in all Unix operating system flavors and variants from
  that point onward including Linux and macOS.

# Mechanism - How it works?

In all Unix and Unix-like systems, each process has its own separate set
of environment variables.
- At the API level, when a new executable is loaded to replace an old
  one via `execve` system call, kernel gives it environment passed in
  `envp` parameter of the system call.
- Usually, old executable gives a duplicate of its own environment to
  the new one (`execv`, `execl`, and `execvp` flavors of that system
  call do this automatically), but old executable can either change its
  own environment before "executing", or pass a custom `envp` to
  `execve`.
    + Invoke a new shell without passing environment variables
        * `$ env -i bash`

# Use and display

Something

# Assignment

Something

# List of environment variables and locations

	MANPATH
	BROWSER
	SYSTEM
	LANG
	LC_MESSAGES
	SSH_AGENT_PID
	SSH_AUTH_SOCK
	SSH_KEY_PATH
	SHELL
	TERM
	ZSH
	USER
	PAGER
	LSCOLORS
	PATH
	MAIL
	PWD
	OLDPWD
	EDITOR
	HOME
	LESS
	ARCHFLAGS
	DISPLAY
	XDG_RUNTIME_DIR
	XAUTHORITY
	_

# References

[wiki]: https://en.wikipedia.org/wiki/Environment_variable
[awiki]: https://wiki.archlinux.org/index.php/Environment_variables
