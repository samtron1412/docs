[TOC]

# Overview
**Unix** (all-caps **UNIX** for the trademark) is a family of **multitasking**, **multiuser** computer operating systems that derive from the original AT&T Unix, developed in the 1970s at the Bell Labs research center by *Ken Thompson*, *Dennis Ritchie*, and others

Written in **C** and assembly language. Historically **closed source**. Development started in 1969, First manual published internally in 1971, announced outside Bell Labs in 1973. Kernel type **monolithic**.

# History
![history](../graphic/unix/Unix-history-simple.svg)

# [UNIX philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)

# Components
## Kernel
source code in /usr/sys, composed of several sub-components:
- **conf** – configuration and machine-dependent parts, including boot code
- **dev** – device drivers for control of hardware (and some pseudo-hardware)
- **sys** – operating system "kernel", handling memory management, process scheduling, system calls, etc.
- **h** – header files, defining key structures within the system and important system-specific invariables

## Development Environment
early versions of Unix contained a development environment sufficient to recreate the entire system from source code:
- **cc** – C language compiler (first appeared in V3 Unix)
- **as** – machine-language assembler for the machine
- **ld** – linker, for combining object files
- **lib** – object-code libraries (installed in /lib or /usr/lib). libc, the system library with C run-time support, was the primary library, but there have always been additional libraries for such things as mathematical functions (libm) or database access. V7 Unix introduced the first version of the modern "Standard I/O" library stdio as part of the system library. Later implementations increased the number of libraries significantly.
- **make** – build manager (introduced in PWB/UNIX), for effectively automating the build process
- **include** – header files for software development, defining standard interfaces and system invariants
- **Other languages** – V7 Unix contained a Fortran-77 compiler, a programmable arbitrary-precision calculator (bc, dc), and the **awk** scripting language; later versions and implementations contain many other language compilers and toolsets. Early BSD releases included Pascal tools, and many modern Unix systems also include the GNU Compiler Collection as well as or instead of a proprietary compiler system.
- **Other tools** – including an object-code archive manager (ar), symbol-table lister (nm), compiler-development tools (e.g. lex & yacc), and debugging tools.

## Commands
Unix makes little distinction between commands (user-level programs) for system operation and maintenance (e.g. cron), commands of general utility (e.g. grep), and more general-purpose applications such as the text formatting and typesetting package. Nonetheless, some major categories are:
- **sh** – the "shell" programmable command-line interpreter, the primary user interface on Unix before window systems appeared, and even afterward (within a "command window").
- **Utilities** – the core toolkit of the Unix command set, including *cp, ls, grep, find* and many others. Subcategories include:
	+ **System utilities** – administrative tools such as **mkfs**, **fsck**, and many others.
	+ **User utilities** – environment management tools such as *passwd, kill*, and others.
- **Document formatting** – Unix systems were used from the outset for document preparation and typesetting systems, and included many related programs such as *nroff, troff, tbl, eqn, refer, and pic*. Some modern Unix systems also include packages such as TeX and Ghostscript.
- **Graphics** – the plot subsystem provided facilities for producing simple vector plots in a device-independent format, with device-specific interpreters to display such files. Modern Unix systems also generally include X11 as a standard windowing system and GUI, and many support **OpenGL**.
- **Communications** – early Unix systems contained no inter-system communication, but did include the inter-user communication programs mail and write. V7 introduced the early inter-system communication system UUCP, and systems beginning with BSD release 4.1c included TCP/IP utilities.

## Documentation
Unix was the first operating system to include all of its documentation online in machine-readable form. The documentation included:
- **man** – manual pages for each command, library component, system call, header file, etc.
- **doc** – longer documents detailing major subsystems, such as the C language and troff

# Standards
## Portable Operating System Interface - [POSIX](https://en.wikipedia.org/wiki/POSIX)
POSIX  is a family of standards specified by the IEEE Computer Society for maintaining compatibility between operating systems.

## Executable and Linkable Format ([ELF](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format))
ELF is a common standard file format for executables, object code, shared libraries, and core dumps.
### File layout

### Tools

### Applications


## [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)
The FHS defines the **directory structure** and **directory contents** in Unix and Unix-like operating systems, maintained by the Linux Foundation.


# Distro
- Archlinux
- Gentoo
- FreeBSD
- OpenBSD
- Minix
- Mac OS X
