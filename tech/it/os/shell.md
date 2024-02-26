[TOC]

# Overview

In computing, a shell is **a user interface** for access to an operating
system's services. In general, operating system shells use either a
command-line interface (CLI) or graphical user interface (GUI),
depending on a computer's role and particular operation.

The shell runs inside a terminal, virtual terminal or terminal emulator.

We can use shell to **programming**.

![Design Shell](shell/Linux_kernel_and_gaming_input-output_latency.svg "Design shell")


# Text shells (Command line interface - CLI)

- [List of CLI](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)

## [Unix-like systems](https://en.wikipedia.org/wiki/Unix_shell)

- `sh` vs `bash`:
    + https://stackoverflow.com/questions/5725296/difference-between-sh-and-bash
    + `sh` is a programming language described by the POSIX standard. It
      has many implementations (`ksh88`, `dash`, ...)
        * Because `sh` is a specification, not an implementation,
          `/bin/sh` is a symlink (or a hard link) to an actual
          implementation on most POSIX systems.
    + `bash` started as an `sh`-compatible implementation, however, over
      time it has acquired many extensions, and it is no longer
      POSIX-compliant.
        * `bash` supports a `--posix` switch, which makes it more
          POSIX-compliant.
- [Bourne shell (sh)](https://en.wikipedia.org/wiki/Bourne_shell): first UNIX shell written by [Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson_(computer_programmer))
  + [Bourne-Again shell (bash)](https://en.wikipedia.org/wiki/Bash_(Unix_shell)): GNU project
  + [Z shell (zsh)](https://en.wikipedia.org/wiki/Z_shell): a relatively modern shell that is backward compatible with bash.
- [C shell](https://en.wikipedia.org/wiki/C_shell): added command history, arithmetic, and other features compare with sh
- Shell script portability with shebang
    + https://serverfault.com/questions/865874/bin-sh-vs-bin-bash-for-maximum-portability
    + Most portable: `#!/bin/sh` + POSIX standard syntax
    + Second most portable: `#!/bin/bash` + bash v3 syntax
    + Third most portable: `#!/bin/bash` + bash v4 features
    + Least portable: `#!/bin/zsh` + specific syntax
    + WRONG: `#!/bin/sh` + non POSIX syntax


## BSD


## Windows



# Graphical shells

## [Microsoft Windows](https://en.wikipedia.org/wiki/Windows_shell)

## Unix-like systems

[Windowing system](https://en.wikipedia.org/wiki/Windowing_system)

## BSD

# Terminology

## sh-like shell system - Interactive vs non-Interactive and Login vs non-Login

> Why need more type of shell like this? Because some configurations
> only need load once, e.g. system configurations, some configuration
> need load every invoke a new shell, e.g. user configurations, and some
> shell is interactive with user, some only are used for scripting.

We can have 4 different types of shells:

1. Interactive login shells,
2. Non-interactive login shells,
3. Interactive non-login shells,
4. Non-interactive non-login shells

- Interactive shells: users type commands and wait for results
- Non-interactive shells: scripting
- Login shells: invoke when users log in to a system

> Users can change the type of shell

# Shell configuration files

- `/etc/profile`: the system wide initialization file, executed for
  *login shells*
- `~/.bash_profile`: the personal initialization file, executed for
  *login shells*. Run **bashrc** before run something else.
- `~/.bashrc`: the individual *per-interactive-shell* start up file

# Bash

## Readline library

- Common library for line editing.

| Keyboard Shortcut | Description                                       |
|-------------------|---------------------------------------------------|
| Ctrl+l            | Clear the screen                                  |
| Cursor Movement   |
| Ctrl+b            | Move cursor one character to the left             |
| Ctrl+f            | Move cursor one character to the right            |
| Alt+b             | Move cursor one word to the left                  |
| Alt+f             | Move cursor one word to the right                 |
| Ctrl+a            | Move cursor to start of the line                  |
| Ctrl+e            | Move cursor to end of the line                    |
| Copy & Paste      |
| Ctrl+u            | Cut everything from line start to cursor          |
| Ctrl+k            | Cut everything from the cursor to end of the line |
| Alt+d             | Cut the current word after the cursor             |
| Ctrl+w            | Cut the current word before the cursor            |
| Ctrl+y            | Paste the previous cut text                       |
| Alt+y             | Paste the second latest cut text                  |
| Alt+Ctrl+y        | Paste the first argument of the previous command  |
| Alt+./_           | Paste the last argument of the previous command   |
| History           |
| Ctrl+p            | Move to the previous line                         |
| Ctrl+n            | Move to the next line                             |
| Ctrl+s            | Search                                            |
| Ctrl+r            | Reverse search                                    |
| Ctrl+j            | End search                                        |
| Ctrl+g            | Abort search (restores original line)             |
| Alt+r             | Restores all changes made to line                 |
| Completion        |
| Tab               | Auto-complete a name                              |
| Alt+?             | List all possible completions                     |
| Alt+*             | Insert all possible completions                   |

# Basic shell script

- More details in `shell-scripts.md`
- The shell script need locate in the directories listed in the PATH
  variables if you want run the script by name.
- If the script do not have execute permission we need user command like
  this to run script: `$ bash <path to script>`
    + After set execute permission for the script:
        * `# chmod +x <path to script>`
    + We can run script by name: `$ <script name>`
- Should write the shell scripts by text editor such as: Sublime Text,
  vim, Emacs, etc. Because they don't store meta information out of text
  contents.
- Basic template shell script:

```shell
#!/bin/bash
#: Title                                : hw
#: Date                                 : 2015 - 06 - 25
#: Author                               : "Thaison Tranhuynh" <samtron1412@gmail.com>
#: Version                      : 1.0
#: Description  : print Hello, World!
#: Options                      : None

printf '%s\n' "Hello, World!"
```

- In shell script we should use `hash(#)` to comment, we should add a
  character after the hash to indicate the type of comment. E.g `#:` is
  comment of the shell script file, `#::` is comment of the function,
  `#:::` is comment for variables or code blocks.

# Tips and Tricks

## [Shell templates](https://github.com/RenatGilmanov/shell-script-template)

# References

[wiki]: https://en.wikipedia.org/wiki/Shell_(computing)
[awiki]: https://wiki.archlinux.org/index.php/Command-line_shell

