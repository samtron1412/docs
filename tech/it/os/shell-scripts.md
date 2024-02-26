# Overview

A collection of tasks that can be solved quickly with shell scripts.

# Search text files

- `ripgrep`: `grep.md`

# Read/search compressed text file on a fly

Make sure the files have the correct extensions (not required for some
file types, but to simplify the things to remember, just change the file
names with correct extensions). Take a look at the rename multiple file
section for detailed steps.

- Using `ripgrep -z`
- Using `z*` commands
    + https://www.cyberciti.biz/tips/decompress-and-expand-text-files.html

# Rename multiple files

- https://linuxconfig.org/how-to-rename-multiple-files-on-linux
    + `for i in *; do mv $i $i.gz ; done`
    + `find . -type f -name 'file*' -print0 | xargs --null -I{} mv {} {}.bak`
    + `find . -name "*.txt" -exec mv {} {}_backup \;`
    + `ls *.txt | xargs -I{} mv {} {}_backup`
- `rename` command
- `mmv` command

# Decompressed files

- https://unix.stackexchange.com/questions/94837/having-trouble-uncompressing-a-few-files
    + `unzip`, `unrar`, `gunzip`, `tar`

# POSIX compliant scripts

- Using shellcheck plugins in IDEs/Editor to help with writing
  POSIX-compliant scripts that can be used in any UNIX/Linux systems.
- Single quotes vs double quotes
    + Single Quotes: Preserve text exactly as is, no variable or command
      substitution, and minimal interpretation of special
      characters. Used for literal strings.
    + Double Quotes: Allow variable and command substitution, preserve
      spaces and most special characters, and expand variables within
      the string.

# Common commands

# export

- To summarize, `export` in shell scripting is used to share variables and
  functions with child processes, making them accessible to subshells,
  scripts, and programs that are executed from within the script. This
  is a fundamental mechanism for inter-process communication and
  configuration management in shell scripting.
- It's important to note that variables exported in a script are only
  available to child processes and not to the parent or other unrelated
  processes. When the child process exits, the exported
  variables/functions do not affect the parent process.
