[TOC]

# Overview
man page (short for manual page) is a form of software documentation usually found on a UNIX or UNIX-like operating system. Topics covered include computer programs (including library and system calls), formal standards and conventions, and even abstract concepts. A user may invoke a man page by issuing the `man <command-name>` or `man <section> <command-name>`.

By default, `man` uses a terminal pager program such as `more` or `less` to display its content.

## History
- In the first two years of the history of UNIX, no documentation existed.
- The UNIX Programmer's Manual was first published on November 3, 1971.
- The first actual man pages were written by Dennis Ritchie and Ken Thompson at the insistence of their manager Doug Mcllroy in 1971.
- The modern descendants of 4.4BSD replaced the old `-man` macros with the newer `-mdoc`.
- The default format of the man pages is **troff**, with either the **macro package** man (appearance oriented) or **mdoc** (semantic oriented). This makes it possible to typeset a man page into PostScript, PDF, and various other formats for viewing and printing.
- In 2010, OpenBSD deprecated troff for formatting manpages in favor of mandoc, a specialized compiler/formatter for manpages with native support for output in PostScript, HTML, XHTML, and the terminal.
