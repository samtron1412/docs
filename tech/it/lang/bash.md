[TOC]

# Overview

## Resources

- Bash reference manual / Bash Features:
    + https://www.gnu.org/software/bash/manual/bash.html
    + https://www.gnu.org/software/bash/manual/html_node/index.html
- Wiki: https://en.wikipedia.org/wiki/Bash_(Unix_shell)
- Bash Guide for Beginners
    + http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html
- Advanced Bash-Scripting Guide
    + http://tldp.org/LDP/abs/html/index.html
- Style guide
    + https://google.github.io/styleguide/shellguide.html
- Naming conventions
    + https://google.github.io/styleguide/shellguide.html#s7-naming-conventions
    + https://stackoverflow.com/questions/673055/correct-bash-and-shell-script-variable-capitalization
    + https://unix.stackexchange.com/questions/42847/are-there-naming-conventions-for-variables-in-shell-scripts
- List all built-in commands: `compgen`
- Check type of a command (is it internal command (built-in) or
  external)
    + `type [-a] cmd`: `type -a top`
    + `command -V cmd`: `command -V top`
    + Output: `top is a shell builtin`
- Find the command executable location:
    + `where cmd`:
    + `which cmd`

# Variables

- With or without `export`:
    + https://www.baeldung.com/linux/bash-variables-export

# Built-in Commands

## sh built-in commands


## bash built-in commands


# stdin, stdout, stderr

- File descriptors:
    + stdin: 0
    + stdout: 1
    + stderr: 2
- Redirect both command output and errors to a file
    + `cmd > file.txt 2>&1`


# Conditions in bash scripting (if statements)

- https://acloudguru.com/blog/engineering/conditions-in-bash-scripting-if-statements

# Shell Parameter

- https://www.gnu.org/software/bash/manual/html_node/Shell-Parameters.html

## Introduction

A parameter is an entity that stores values.

There are three types of parameters:
- Positional Parameters: are arguments present on the command line, and
  they are referenced by number.
- Special Parameters: set by the shell to store information about
  aspects of its current state, such as the number of arguments and the
  exit code of the last command. Their name is nonalphanumeric
  characters (for example, `*`, `#`, `_`).
- Variables: are identified by a name.

The value of a parameter is accessed by preceding its name, number, or
character with a dollar sign (`$`), as in `$3`, `$#`, `$HOME`. The name
may be surrounded by braces, as in `${10}`, `${PWD}`, or `${USER}`,
braces is much use with array `${array[@]}`

- Nameref
    + https://stackoverflow.com/questions/40593740/can-namerefs-declare-n-be-used-with-arrays-in-bash-what-does-the-documentati

## Positional Parameters

The arguments on the command line are available to a shell program as
numbered parameters. The first argument is `$1`, the second is `$2`, and
so on.

The Bourne shell(sh) could only address up to nine positional
parameters. To access positional parameters greater than 9, the number
must be enclosed in braces: `${15}`.

## Special Parameters

- The first two special parameters, `$*` and `$@`, expand to the value
  of all the positional parameters combined.
- `$#`: expands to the number of positional parameters.
- `$0`: contains the path to the currently running script or to the
  shell itself if no script is being executed.
- `$$` contains the process identification number (PID) of the current
  process.
- `$?` is set to the exit code of the last-executed command.
- `$_` is set to the last argument to that command.
- `$!` contains the PID of the last command executed in the background.
- `$-` is set to the option flags currently in effect.

## Variables

A variable is a parameter denoted by a name; a name is a word containing
only letters, numbers, or underscores and beginning with a letter or an
underscore.

Value can be assigned to variables in the following form: `name=VALUE`

Many variables are set by the shell itself, all the variables set by the
shell are all uppercase letters.

## Arguments and Options

The words entered **after the command** are its arguments. These are
words separated by whitespace **(one or more spaces or tabs)**. If the
whitespace is escaped or quoted, it no longer separates words but
becomes part of the word.

The following command lines all have four arguments:

```bash
echo 1 '2   3'   4 5
echo  -n  Now\ is  the  time
printf '%s %s\n' one two three
```

In the first line, the spaces between 2 and 3 are quoted because they
are surrounded by single quotation marks. In the second, the space after
`Now` is escaped by a *backslash(`\`)*, which is the shell's escaped
character.

In the final line, a space is quoted with single quotes.

In the second line, the first arguments is an option. Traditionally,
options to Unix commands are a single letter preceded by a hyphen,
sometimes followed by an argument.

The GNU commands found in Linux distributions often accept **long
options** as well. These are words preceded by a double hyphen.

## Parsing shell parameter (long form allowable) with getopt

- https://www.shellscript.sh/tips/getopt/index.html

# Shell Expansion

- https://www.gnu.org/software/bash/manual/html_node/Shell-Expansions.html

# Array

- https://linuxize.com/post/bash-arrays/

# Error Handling

- https://stackoverflow.com/questions/64786/error-handling-in-bash
- http://mywiki.wooledge.org/BashFAQ/105
- https://github.com/Privex/shell-core
- https://stackoverflow.com/questions/22009364/is-there-a-try-catch-command-in-bash
- https://www.redhat.com/sysadmin/bash-error-handling
- https://linuxcommand.org/lc3_wss0140.php
- https://linuxhint.com/bash_error_handling/
- https://www.xmodulo.com/catch-handle-errors-bash.html
- https://dev.to/banks/stop-ignoring-errors-in-bash-3co5
- https://medium.com/@dirk.avery/the-bash-trap-trap-ce6083f36700

# Temporary

- [Here document](https://en.wikipedia.org/wiki/Here_document#Unix-Shells): EOF, STOP
- [How to call shell script from another shell script?](https://stackoverflow.com/questions/8352851/how-to-call-shell-script-from-another-shell-script)
    + There are a couple of ways you can do this:
        * The first is to **make the other script executable**, add the
          `#!/bin/bash` line at the top, and the path where the file is
          to the `$PATH` environment variable. Then you can call it as a
          normal command.
        * Call it with the `source` command (alias is `.`) like this:
          `source /path/to/script`.
        * Use the `bash` command to execute it: `/bin/bash
          /path/to/script`.
    + The first and third methods execute the script as another process,
      so variables and functions in the other script will not be
      accessible. The second method executes the script in the first
      scripts process, and pulls in variables and functions from the
      other script so they are usable from the calling script.
- [How to include bash script file](https://stackoverflow.com/questions/192292/bash-how-best-to-include-other-scripts)

```man.sh
#!/bin/bash
my_dir="$(dirname "$0")"
source "$my_dir/incl.sh"
echo "The main script"
```

```incl.sh
#!/bin/bash
echo "The included script"
```

- [Try catch](https://stackoverflow.com/questions/22009364/is-there-a-try-catch-command-in-bash)
- [Template](https://stackoverflow.com/questions/14008125/shell-script-common-template)
- [Get length of array](http://www.cyberciti.biz/faq/finding-bash-shell-array-length-elements/)
- [printf](http://wiki.bash-hackers.org/commands/builtin/printf)
- [Parameter substitution](http://www.tldp.org/LDP/abs/html/parameter-substitution.html)


# Arrays and Associative Arrays (bash v4+)

- https://www.baeldung.com/linux/bash-array

# If Statements

- https://linuxize.com/post/bash-if-else-statement/

## Check if an environment variable exists

- https://stackoverflow.com/questions/39296472/how-to-check-if-an-environment-variable-exists-and-get-its-value
- https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameter-Expansion

```sh
if [[ -z "${DEPLOY_ENV}" ]]; then
  MY_SCRIPT_VARIABLE="Some default value because DEPLOY_ENV is undefined"
else
  MY_SCRIPT_VARIABLE="${DEPLOY_ENV}"
fi

# or using a short-hand version

[[ -z "${DEPLOY_ENV}" ]] && MyVar='default' || MyVar="${DEPLOY_ENV}"

# or even shorter use

MyVar="${DEPLOY_ENV:-default_value}"
```

## Check if a program exists

- https://stackoverflow.com/questions/592620/how-can-i-check-if-a-program-exists-from-a-bash-script

```bash
if ! command -v <the_command> &> /dev/null
then
    echo "<the_command> could not be found"
    exit
fi
```

## Check if string equal condition

- https://linuxize.com/post/how-to-compare-strings-in-bash/
- https://stackoverflow.com/questions/4277665/how-do-i-compare-two-string-variables-in-an-if-statement-in-bash
- https://stackoverflow.com/questions/2237080/how-to-compare-strings-in-bash

```bash
if [ "${x1}" = "${x2}" ]; then
    echo abc
fi
```

# Loops

## For loops

- `continue` and `break`
    + https://linuxize.com/post/bash-break-continue/


# Functions

- https://linuxize.com/post/bash-functions/


# Best Practices and Guides

- https://google.github.io/styleguide/shellguide.html
- https://github.com/icy/bash-coding-style
- Quote string variables if you don't want word splitting and wildcard
  expansion
    + `"${some_var}"`
- When to use curly braces around variables?
    + https://stackoverflow.com/questions/8748831/when-do-we-need-curly-braces-around-shell-variables
    + Should develop the habit of using `{}` for every variable.
- Command substitution
    + `$(command)`
- Quotes inside quotes
    + https://stackoverflow.com/questions/3834839/how-can-i-escape-a-double-quote-inside-double-quotes

# Tips and Tricks

## To lowercase

- https://stackoverflow.com/questions/2264428/how-to-convert-a-string-to-lower-case-in-bash

## Working with JSON

- https://stackoverflow.com/questions/43373176/store-json-directly-in-bash-script-with-variables

## Set text color in the terminal

- https://unix.stackexchange.com/a/269085/68026
- `tput`

```
RED=$(tput setaf 1)
GREEN=$(tput setaf 2)
OFF=$(tput sgr0)

echo "${GREEN}Created diff.txt!"
echo
echo "On a Cloud Desktop, create a paste by running:"
echo
echo "/apollo/env/envImprovement/bin/paste.amazon.com diff.txt"
echo
echo "On macOS, create a paste at https://paste.amazon.com."
echo "You can copy the file to the clipboard by running:"
echo
echo "pbcopy < diff.txt${OFF}"
```


## References in bash

- https://newbedev.com/does-bash-provide-support-for-using-pointers
- Array or associative array
- Indirect expansion: `${!var}`
    + `!var` is expanded into the value of `var`, then `${var_value}` is
      expanded
- Namerefs: `declare -n ref=var` makes `ref` a reference to the variable
  `var`

## Search the command history

- `Ctrl + R` -> start typing -> once the result appears keep hitting
  `Ctrl + R` to see other matches
    + `Enter` to run the command or arrow keys to move and edit the
      command
- Rebind the command `reverse-search-history`
    + `bind '"\C-t": reverse-search-history'`
- Alternative to `Ctrl + R`
    + search history by typing `!<text>`: this will search the history
      for the most recent command beginning with 'text'
    + put `shopt -s histverify` in your .bashrc to prevent execution of
      wrong command
      => this will places the resulting line to the command prompt then
      you can review or edit the command
