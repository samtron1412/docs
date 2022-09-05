[TOC]

# Overview
- Recursively grep through directory for string in file: `grep -r -i "phrase" directory/`

# Tips and Tricks

## Finding all files containing a text string on Linux

`grep -Ril "text-to-find-here" /`
	i stands for ignore case (optional in your case).
	R stands for recursive.
	l stands for "show the file name, not the result itself".
	/ stands for starting at the root of your machine.

`grep -rnw '/path/to/somewhere/' -e "pattern"`
-r or -R is recursive,
-n is line number, and
-w stands match the whole word.
-l (lower-case L) can be added to just give the file name of matching files.

Along with these, --exclude or --include parameter could be used for efficient searching. Something like below:
`grep --include=\*.{c,h} -rnw '/path/to/somewhere/' -e "pattern"`
This will only search through the files which have .c or .h extensions. Similarly a sample use of --exclude:

`grep --exclude=*.o -rnw '/path/to/somewhere/' -e "pattern"`
Above will exclude searching all the files ending with .o extension. Just like exclude file it's possible to exclude/include directories through --exclude-dir and --include-dir parameter; for example, the following shows how to integrate --exclude-dir:

`grep --exclude-dir={dir1,dir2,*.dst} -rnw '/path/to/somewhere/' -e "pattern"`

# ripgrep (rg command)

- Much faster than `grep`
- Search a string in a file: `rg "string" a.file`
- Search each string in each line in a file in another larger file:
    + `rg -F -f pattern-file large-file`
- Only show matched patterns (not the whole line) `-o`
    + `rg -Fo -f pattern-file large-file`
