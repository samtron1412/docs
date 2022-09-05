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
