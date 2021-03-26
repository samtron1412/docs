[TOC]

# Overview

The Z shell (zsh) is a **Unix shell**. Zsh can be thought of as an
extended Bourne shell with a large number of improvements, including
some features of bash, ksh, and tcsh. It offers many advantages such as:

- Efficiency
- Improved tab completion
- Improved globbing (specify sets of filename with wildcard characters)
- Improved array handling
- Full customisability

**Paul Falstad** wrote the first version of zsh in 1990 while a student
at Princeton University

# Configuration files

When starting Zsh, it'll source the following files in this order by
default:

- `/etc/zsh/zshenv`:
    + This file should contain commands to set the global command search
      path and other system-wide environment variables; it should not
      contain commands that produce output or assume the shell is
      attached to a tty.
- `~/.zshenv`: always sourced
    + Similar to /etc/zsh/zshenv but for per-user configuration.
      Generally used for setting some useful environment variables.
- `/etc/zsh/zprofile`:
    + This is a global configuration file, it'll be sourced at login.
      Usually used for executing some general commands at login. Please
      note that on Arch Linux, by default it contains one line which
      source the `/etc/profile`.
- `/etc/profile`:
    + This file should be sourced by all Bourne-compatible shells upon
      login: it sets up an environment upon login and application-
      specific (`/etc/profile.d/*.sh`) settings. Note that on Arch
      Linux, Zsh will also source this by default.
- `~/.zprofile`: source at login before zshrc
    + This file is generally used for automatic execution of user's
      scripts at login.
- `/etc/zsh/zshrc`:
    + Global configuration file, will be sourced when starting as a
      interactive shell.
- `~/.zshrc`: interactive shell
    + Main user configuration file, will be sourced when starting as a
      interactive shell.
- `/etc/zsh/zlogin`:
    + A global configuration file, will be sourced at the ending of
      initial progress when starting as a login shell.
- `~/.zlogin`: sourced at login after zshrc
    + Same as /etc/zsh/zlogin but for per-user configuration.
- `/etc/zsh/zlogout`:
    + A global configuration file, will be sourced when a login shell
      exits.
- `~/.zlogout`:
    + Same as /etc/zsh/zlogout but for per-user configuration.

>**Note**:
- The paths used in Arch's zsh package are different from the default
  ones used in the man pages
- `/etc/profile` is not a part of the regular list of startup files run
  for Zsh, but is sourced from `/etc/zsh/zprofile` in the zsh package.
  Users should take note that `/etc/profile` sets the **$PATH** variable
  which will overwrite any **$PATH** variable set in `~/.zshenv`. To
  prevent this, please set the **$PATH** variable in `~/.zprofile`

>**Warning**: It is not recommended to replace the default one line in
>`/etc/zsh/zprofile` with something other, it'll break the integrality
>of other packages which provide some scripts in `/etc/profile.d`

## .zshenv

_[Read every time]_

It is always sourced, so it should set environment variables which need
to be **updated frequently**. _PATH_ (or its associated counterpart
_path_) is a good example because you probably don't want to restart
your whole session to make it update. By setting it in that file,
reopening a terminal emulator will start a new Zsh instance with the
_PATH_ value updated.

But be aware that this file is **read even when Zsh is launched to run a
single command** (with the _-c_ option), even by another tool like
`make`. You should **be very careful to not modify the default behavior
of standard commands** as it may break some tools which use them (by
setting aliases for example). For sure, it is not forbidden as you know
what you are doing.

## .zprofile

_[Read at login]_

I personally treat that file like `.zshenv` but for commands and
variables which should be set once or which **don't need to be updated
frequently**:

 - environment variables to configure tools (flags for compilation, data
 folder location, etc.) - configuration which execute commands (like
 `SCONSFLAGS="--jobs=$(( $(nproc) - 1 ))"`) as it may take some time to
 execute.

If you modify that file, you can get the configuration updates by
replacing the current shell with a new one as login shell:

    exec zsh --login

## .zshrc

_[Read when interactive]_

I put here everything needed only for **interactive usage**:

 - prompt,
 - command completion,
 - command correction,
 - command suggestion,
 - command highlighting,
 - output coloring,
 - aliases,
 - key bindings,
 - commands history management,
 - other miscellaneous interactive tools (auto_cd, manydots-magic)...

## .zlogin

_[Read at login]_

This file is like `.zshprofile`, but is read after `.zshrc`. I consider
the shell to be fully set up at this time.

So, I use it to launch external commands which do not modify the shell
behaviors (e.g. a login manager).

## .zlogout

_[Read at logout][Within login shell]_

Here, you can clear your terminal or any other resource setup at login.

## How I choose where to put a setting

 - it is needed by a **command run non-interactively**: `.zshenv`
 - it should be **updated on new shell**: `.zshenv`
 - it runs a command which **may take some time to complete**: `.zprofile`
 - it is related to **interactive usage**: `.zshrc`
 - it is a **command to be run when the shell is fully setup**: `.zlogin`
 - it **releases a resource** acquired at login: `.zlogout`


# Configuring ZSH

## Configure environment variables

- `$PATH`
- `$EDITOR`
- `$GIT_EDITOR`
- `$SAVEHIST`
- `$LSCOLORS`
- `$LS_COLORS`
- `$GPG_TTY`
- `$GPG_AGENT_INFO`

# Configuration frameworks

- It adds a layer of abstraction to ZSH configuration

## [oh-my-zsh](http://ohmyz.sh/)

`lib`: contain many useful library for zsh. Read code to understand the
details.
- Add environment variables
- Completion, git branches, correction, etc.

## prezto

- https://github.com/sorin-ionescu/prezto

# Plugin managers

- It manages all plugins, including plugins in configuration frameworks
  such as oh-my-zsh.

## Manually manage plugins

- Research more this option.
- Potentially fastest.

## zinit

- https://github.com/zdharma/zinit

## antigen

- https://github.com/zsh-users/antigen

## zplug

# Plugins

## Resources

- https://github.com/unixorn/awesome-zsh-plugins

## git

- add many aliases and functions

## [z](https://github.com/rupa/z)

- Jump to places based on frequency
- `z foo`

## vi-mode

- vi-like functionality
- manual:
   + https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/vi-mode
   + `ctrl-p` or `k`: previous command
   + `ctrl-n` or `j`: next command
   + `/`: search backward
   + `n`: repeat the last `/`

## history-substring-search

- typing part of a command and using UP, DOWN or `k`, `j` to match
  commands in the history
- VERY USEFUL

## jump

- jumps around the file system by manually adding marks

```
# jump FOO: jump to a mark named FOO
# mark FOO: create a mark named FOO
# unmark FOO: delete a mark
# marks: lists all marks
```


## Theme

- robbyrussell

## zsh-syntax-highlighting

- https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md

# Improve performance

## Total runtime

- Total runtime for bare ZSH: `time zsh -df -c echo`
- Total runtime for interactive ZSH: `time zsh -i -c echo`

## Profiling ZSH

- Add the following code to the top of .zshrc

```zsh
zmodload zsh/datetime
setopt PROMPT_SUBST
PS4='+$EPOCHREALTIME %N:%i> '

logfile=$(mktemp zsh_profile.XXXXXXXX)
echo "Logging to $logfile"
exec 3>&2 2>$logfile

setopt XTRACE
```

- Add this code to the bottom:

```zsh
unsetopt XTRACE
exec 2>&3 3>&-
```

Now if you create a new zsh instance you’ll have a file called something
like “zsh_profile.abcd1234” in your home directory. Copy the following
script into a file called “sort_timings.zsh” and make it executable:

```zsh
#!/usr/bin/env zsh

# Takes a list of commands with timing information and lists the commands from
# longest- to shortest-running.
#
# The script reads from the filename given on the command line, or from
# standard input if no filename is given. The input is expected to look like
#
#     +1518804574.3228740692 colors:76> local k
#     +1518804574.3228929043 colors:77> k=44
#     +1518804574.3229091167 colors:77> color[${color[$k]}]=44
#     +1518804574.3229229450 colors:77> k=33
#     +1518804574.3229279518 colors:77> color[${color[$k]}]=33
#
# Everything between the leading "+" and the next space is taken to be a
# decimal number of seconds with at least microsecond precision (i.e., at least
# six digits after the decimal point). Additional digits are allowed but
# ignored. The rest of the line does not need to be in any particular format,
# but the script will truncate this portion of the line with "..." so that it
# is no longer than 80 characters.
#
# The output will look like
#
#     18 colors:76> local k
#     17 colors:77> k=44
#     13 colors:77> color[${color[$k]}]=44
#     5 colors:77> k=33
#
# The first number on each line is the number of microseconds taken by that
# command. (Depending on how you obtain the timing information, the values may
# or may not actually be accurate to the microsecond. This should still give
# you a good idea of the relative timings, though.)
#
# See https://esham.io/2018/02/zsh-profiling for an explanation of the context
# in which this script is intended to be used.
#
# This script was written by Benjamin Esham (https://esham.io) and is released
# under the following terms:
#
# This is free and unencumbered software released into the public domain.
#
# Anyone is free to copy, modify, publish, use, compile, sell, or distribute
# this software, either in source code form or as a compiled binary, for any
# purpose, commercial or non-commercial, and by any means.
#
# In jurisdictions that recognize copyright laws, the author or authors of this
# software dedicate any and all copyright interest in the software to the
# public domain. We make this dedication for the benefit of the public at large
# and to the detriment of our heirs and successors. We intend this dedication
# to be an overt act of relinquishment in perpetuity of all present and future
# rights to this software under copyright law.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
# ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
# WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
#
# For more information, please refer to <http://unlicense.org/>


typeset -a lines
typeset -i prev_time=0
typeset prev_command

while read line; do
    # Anything between the beginning of the line and the "+" is just ignored.
    #
    # In particular, in cases where one logging line stops abruptly and a new
    # one begins without an intervening newline, the ".*" in this pattern
    # slurps up the incomplete logging line and leaves only the full line that
    # comes after. This kind of thing can happen if your zshrc contains an
    # assignment like now=$(date); the XTRACE module prints a line
    # corresponding to "now=" but then neglects to print a newline before the
    # line corresponding to the "date" command. The net effect is that the
    # report outputted by this script ignores the "now=" part, which shouldn't
    # have taken any time anyway.
    if [[ $line =~ '^.*\+([0-9]{10})\.([0-9]{6})[0-9]* (.+)' ]]; then
        # Form a time in microseconds by concatenating the digits before the
        # decimal point with the first six digits after the decimal point.
        integer this_time=$match[1]$match[2]

        if [[ $prev_time -gt 0 ]]; then
            time_difference=$(( $this_time - $prev_time ))
            lines+="$time_difference $prev_command"
        fi

        prev_time=$this_time

        # If the command is longer than 80 characters, truncate it with "...".
        local this_command=$match[3]
        if [[ ${#this_command} -le 80 ]]; then
            prev_command=$this_command
        else
            prev_command="${this_command:0:77}..."
        fi
    fi
done < ${1:-/dev/stdin}

# The combination "On" means that the elements of $lines are sorted numerically
# in descending order. The "-l" flag means that each element is printed on its
# own line.
print -l ${(@On)lines}
```

- Run the following command:
    + `./sort_timings.zsh zsh_profile.abcd1234 | less`

# Tips and Tricks

## MacOS

- Confirm version and location of zsh
    + `zsh --version`
    + `which zsh`: /usr/local/bin/zsh => brew; /usr/bin => native zsh
- Confirm the current default shell for a user
    + `dscl . -read /Users/$USER UserShell`
    + `.` is short for localhost
- Change shell
    + `dscl . -create /Users/$USER /usr/local/bin/zsh`
    + or you can use `chsh -s /usr/local/bin/zsh`
    + or you can go in : Settings => Users & Groups => right click on
      user name and choose Advanced Options...

# References

[zsh]: http://www.zsh.org/
[wiki]: https://en.wikipedia.org/wiki/Z_shell
[awesome-zsh]: https://github.com/unixorn/awesome-zsh-plugins
