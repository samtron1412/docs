[TOC]

# Overview

The GNU Compiler Collection (GCC) is a compiler system produced by the
GNU Project supporting various programming languages.

## History

- Founder: Richard Stallman
- First release in March 22, 1987, available by FTP from MIT.

# Design

- GCC's front ends follows Unix conventions. Users invoke a
language-specific driver program (gcc for C, g++ for C++, etc.), which
interprets command arguments, calls the actual compiler, runs the
assembler on the output, and then optionally runs the linker to produce
a complete executable binary.
- Source code -> Front end -> abstract syntax tree -> RTL (intermediate
representation) -> architecture-specific pattern matching -> machine
code.

## Front ends

- Each front end uses a parser to produce the abstract syntax tree of a
given source file. Due to the syntax tree abstraction, source files of
different languages can be processed by the same back end.
- Currently all front ends use hand-written recursive-descent parsers.

## GENERIC and GIMPLE

- GENERIC is an intermediate representation. GIMPLE is a simplified
version of GENERIC.
- All the front ends produces GENERIC.
- The middle stage of GCC does all of the code analysis and
optimization, working independently of both the compiled language and
the target architecture, starting from the GENERIC and producing
register transfer language (RTL).

## Optimization

- Optimization can occur during any phase of compilation; however, the
bulk of optimizations are performed after the syntax and semantic
analysis of the front end and before the code generation of the back
end.

## Back end

# References

[gcc]: https://gcc.gnu.org/
