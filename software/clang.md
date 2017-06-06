[TOC]

# Overview

- Clang is a compiler front end for the programming language C, C++,
Objective-C, Objective-C++, OpenMP, OpenCL, and CUDA.
- It uses LLVM as its back end.
- The Clang project includes the Clang front end, the Clang static
analyzer, and several code analysis tools.

# Design

- Clang is intended to work atop LLVM. The combination of Clang and LLVM
provides most of the toolchain to replace the full GCC stack.
- It is built with a library-based design, so Clang is easy to embed
into other applications.
- Clang is designed to retain more information during the compiling
process than GCC, and to preserve the overall form of the original
source.


# References

[clang]: http://clang.llvm.org/
