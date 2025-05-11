[TOC]

# Overview

- Recursively grep through directory for string in file: `grep -r -i "phrase" directory/`
- Cheatsheet
    + https://quickref.me/grep

# zgrep

- Search text in `*.gz` compressed files.
- Search a pattern in many files
    + `zgrep "DependencyFailureException" $(find . -name "*.gz")`
    + `zgrep "DependencyFailureException" $(find . -wholename "*/2*.gz")`
    + `zgrep -A 30 "DependencyFailureException" $(find . -name "*.gz")`

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

Author's blog post: https://blog.burntsushi.net/ripgrep

Some use cases: https://mariusschulz.com/blog/fast-searching-with-ripgrep

- Much faster than `grep`
- Search a string in a file: `rg "string" a.file`
- Search each string in each line in a file in another larger file:
    + Treat each line as fixed strings rather than regular expression
        * `rg -F -f pattern-file large-file`
        * `rg --fixed-strings --file pattern-file large-file`
    + Regular expression
        * `rg -f pattern-file large-file`
- Only show matched patterns (not the whole line) `-o`
    + `rg -Fo -f pattern-file large-file`
- Only show unique results
    + `rg -Fo -f pattern-file large-file | sort | uniq`
