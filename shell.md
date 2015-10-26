[TOC]

# Overview
In computing, a shell is **a user interface** for access to an operating system's services. In general, operating system shells use either a command-line interface (CLI) or graphical user interface (GUI), depending on a computer's role and particular operation.

We can use shell to **programming**.

![Design Shell](shell/Linux_kernel_and_gaming_input-output_latency.svg "Design shell")


# Text shells (Command line interface - CLI)
## [List of CLI](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)
### [Unix-like systems](https://en.wikipedia.org/wiki/Unix_shell)
- [Bourne shell (sh)](https://en.wikipedia.org/wiki/Bourne_shell): first UNIX shell written by [Ken Thompson](https://en.wikipedia.org/wiki/Ken_Thompson_(computer_programmer))
  + [Bourne-Again shell (bash)](https://en.wikipedia.org/wiki/Bash_(Unix_shell)): GNU project
  + [Z shell (zsh)](https://en.wikipedia.org/wiki/Z_shell): a relatively modern shell that is backward compatible with bash.
- [C shell](https://en.wikipedia.org/wiki/C_shell): added command history, arithmetic, and other features compare with sh


### BSD

### Windows


# Graphical shells
## [Microsoft Windows](https://en.wikipedia.org/wiki/Windows_shell)

## Unix-like systems
[Windowing system](https://en.wikipedia.org/wiki/Windowing_system)

## BSD

# Terminology
## Interactive vs non-Interactive

## Login vs non-Login

# Shell configuration files
`/etc/profile`: the system wide initialization file, executed for *login shells*
`~/.bash_profile`: the personal initialization file, executed for *login shells*. Run **bashrc** before run something else.
`~/.bashrc`: the individual *per-interactive-shell* start up file

# Basic
- The shell script need locate in the directories listed in the PATH variables if you want run the script by name.
- If the script do not have execute permission we need user command like this to run script: `$ bash <path to script>`
	+ After set execute permission for the script: `# chmod +x <path to script>`
	+ We can run script by name: `$ <script name>`
- Should write the shell scripts by text editor such as: Sublime Text, vim, Emacs, etc. Because they don't store meta information out of text contents.
- Basic template shell script:

```shell
#!/bin/bash
#: Title				: hw
#: Date					: 2015 - 06 - 25
#: Author				: "Thaison Tranhuynh" <samtron1412@gmail.com>
#: Version			: 1.0
#: Description	: print Hello, World!
#: Options			: None

printf '%s\n' "Hello, World!"
```

- In shell script we should use `hash(#)` to comment, we should add a character after the hash to indicate the type of comment. E.g `#:` is comment of the shell script file, `#::` is comment of the function, `#:::` is comment for variables or code blocks.
