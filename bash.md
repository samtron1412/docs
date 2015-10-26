[TOC]

# Overview

## Resources
- [Bash Guide for Beginners](http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html)
- [Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html/index.html)

# Parameter
A parameter is an entity that stores values.

There are three types of parameters:
- Positional Parameters: are arguments present on the command line, and they are referenced by number.
- Special Parameters: set by the shell to store information about aspects of its current state, such as the number of arguments and the exit code of the last command. Their name is nonalphanumeric characters (for example, `*`, `#`, `_`).
- Variables: are identified by a name.

The value of a parameter is accessed by preceding its name, number, or character with a dollar sign (`$`), as in `$3`, `$#`, `$HOME`. The name may be surrounded by braces, as in `${10}`, `${PWD}`, or `${USER}`, braces is much use with array `${array[@]}`

## Positional Parameters
The arguments on the command line are available to a shell program as numbered parameters. The first argument is `$1`, the second is `$2`, and so on.

The Bourne shell(sh) could only address up to nine positional parameters. To access positional parameters greater than 9, the number must be enclosed in braces: `${15}`.

## Special Parameters
- The first two special parameters, `$*` and `$@`, expand to the value of all the positional parameters combined.
- `$#`: expands to the number of positional parameters.
- `$0`: contains the path to the currently running script or to the shell itself if no script is being executed.
- `$$` contains the process identification number (PID) of the current process.
- `$?` is set to the exit code of the last-executed command.
- `$_` is set to the last argument to that command.
- `$!` contains the PID of the last command executed in the background.
- `$-` is set to the option flags currently in effect.

## Variables
A variable is a parameter denoted by a name; a name is a word containing only letters, numbers, or underscores and beginning with a letter or an underscore.

Value can be assigned to variables in the following form: `name=VALUE`

Many variables are set by the shell itself, all the variables set by the shell are all uppercase letters.

## Arguments and Options
The words entered **after the command** are its arguments. These are words separated by whitespace **(one or more spaces or tabs)**. If the whitespace is escaped or quoted, it no longer separates words but becomes part of the word.

The following command lines all have four arguments:

```bash
echo 1 '2   3'   4 5
echo  -n  Now\ is  the  time
printf '%s %s\n' one two three
```

In the first line, the spaces between 2 and 3 are quoted because they are surrounded by single quotation marks. In the second, the space after `Now` is escaped by a *backslash(`\`)*, which is the shell's escaped character.

In the final line, a space is quoted with single quotes.

In the second line, the first arguments is an option. Traditionally, options to Unix commands are a single letter preceded by a hyphen, sometimes followed by an argument.

The GNU commands found in Linux distributions often accept **long options** as well. These are words preceded by a double hyphen.




# Temporary
- [Here document](https://en.wikipedia.org/wiki/Here_document#Unix-Shells): EOF, STOP
- [How to call shell script from another shell script?](https://stackoverflow.com/questions/8352851/how-to-call-shell-script-from-another-shell-script)

		There are a couple of ways you can do this:

		1. The first is to **make the other script executable**, add the `#!/bin/bash` line at the top, and the path where the file is to the `$PATH` environment variable. Then you can call it as a normal command.

		2. Call it with the `source` command (alias is `.`) like this: `source /path/to/script`.

		3. Use the `bash` command to execute it: `/bin/bash /path/to/script`.

		The first and third methods execute the script as another process, so variables and functions in the other script will not be accessible. The second method executes the script in the first scripts process, and pulls in variables and functions from the other script so they are usable from the calling script.

- [How to include bash script file](https://stackoverflow.com/questions/192292/bash-how-best-to-include-other-scripts)

	**man.sh**

		#!/bin/bash

		my_dir="$(dirname "$0")"

		source "$my_dir/incl.sh"

		echo "The main script"


	**incl.sh**

		#!/bin/bash

		echo "The included script"

- [Try catch](https://stackoverflow.com/questions/22009364/is-there-a-try-catch-command-in-bash)
- [Template](https://stackoverflow.com/questions/14008125/shell-script-common-template)
- [Get length of array](http://www.cyberciti.biz/faq/finding-bash-shell-array-length-elements/)
- [printf](http://wiki.bash-hackers.org/commands/builtin/printf)
- [Parameter substitution](http://www.tldp.org/LDP/abs/html/parameter-substitution.html)

