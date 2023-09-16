# Overview

- `diff` command
    + `man diff`

# Tips and Tricks

## Diffing two big text files

- `sort a.file > a.file.sorted`
- `sort b.file > b.file.sorted`
- `diff --speed-large-files a.file.sorted b.file.sorted > output`
    + Or you can use `comm`: lines common between two files
        * `comm -23 a.file.sorted b.file.sorted > output`: output will
          contain all lines in `a.file.sorted` but not in
          `b.file.sorted`
        * `comm -13 a.file.sorted b.file.sorted > output`: output will
          contain all lines in `b.file.sorted` but not in
          `a.file.sorted`
        * `comm -12 a.file.sorted b.file.sorted > output`: output will
          contain all lines in `b.file.sorted` and `a.file.sorted`

### Checking whether two files have the same content

- https://www.baeldung.com/linux/fastest-check-files-same-content
- `diff -sq file1 file2`
    + `-q`: `--brief` report only when files differ
    + `-s`: `--report-identical-files` report when two files are the same
- `cmp -s file1 file2`
    + `echo $?`: 0 means file contents are the same
