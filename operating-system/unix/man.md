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

# Manual sections
The manual is generally split into eight numbered sections, organized as follows (on Research UNIX, BSD, OS X, and Linux):

| Section | Description                                                                     |
| -       | -                                                                               |
| 1       | Executable programs or shell commands                                           |
| 2       | System calls (functions provided by the kernel)                                 |
| 3       | Library calls (functions within program libraries)                              |
| 4       | Special files ( usually found in `/dev`)                                        |
| 5       | File formats and conventions e.g. `/etc/passwd`                                 |
| 6       | Games                                                                           |
| 7       | Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7) |
| 8       | System administration commands (usually only for root)                          |

On some systems some of the following sections are available:

| Section | Description            |
| -       | -                      |
| 0       | C library header files |
| 9       | Kernel routines        |
| n       | Tcl/Tk keywords        |
| x       | The X Window System    |

Suffix

| Subsection | Description                   |
| -          | -                             |
| p          | POSIX specifications          |
| x          | X Window System documentation |

# Layout
All man pages follow a common layout that is optimized for presentation on a simple ASCII text display, possibly without any form of highlighting or font control. Sections present may include: NAME, SYNOPSIS, CONFIGURATION, DESCRIPTION, OPTIONS, EXIT STATUS, RETURN VALUE, ERRORS, ENVIRONMENT, FILES, VERSIONS, CONFORMING TO, NOTES, BUGS, EXAMPLE, AUTHORS, and SEE ALSO.

| Convention  | Description                                                                                                                                                                                                              |
| NAME        | The name of the command or function, followed by a one-line description of what it does                                                                                                                                  |
| SYNOPSIS    | In the case of a command, a formal description of how to run it and what command line options it takes. For program functions, a list of the parameters the function takes and which header file contains its definition |
| DESCRIPTION | A textual description of the functioning of the command or function                                                                                                                                                      |
| EXAMPLES    | Some examples of common usage                                                                                                                                                                                            |
| SEE ALSO    | A list of related commands or functions                                                                                                                                                                                  |

