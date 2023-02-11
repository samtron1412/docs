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
