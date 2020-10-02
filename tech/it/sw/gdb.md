[TOC]

# Overview

The GNU Debugger (GDB) is a portable debugger that runs on many
Unix-like systems and works for many programming languages.

## History

# Technical details

## Features

## Remote debugging

## Graphical user interface

# Tips and Tricks

## gdb does not stop at breakpoints

- Probably, the breakpoints are set at the child code portion when we
  fork a new process.
- `set follow-fork-mode child`: to debug code in the child
- `set detach-on-fork off`: to let gdb controls both parent and child

# References

[wiki]: https://en.wikipedia.org/wiki/GNU_Debugger
