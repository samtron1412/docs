[TOC]

# Overview

The LLVM compiler infrastructure project (formerly Low Level Virtual
Machine) is a collection of modular and reusable compiler and toolchain
technologies used to develop compiler front ends and back ends.

LLVM is written in C++ and is designed for compile-time, link-time,
run-time, and idle-time optimization of programs written in arbitrary
programming languages.

The LLVM project started in 2000 at the University of Illinois at
Urbaba-Champaign, under the direction of Vikram Adve and Chris Lattner.

# Features

- LLVM can provide the middle layers of a complete compiler system,
  taking intermediate representation (IR) code from a compiler and
  emitting an optimized IR.
- This new optimized IR can then be converted and linked into machine-
  dependent assembly language code for a target platform.
- Clang/GCC front end -> IR -> LLVM -> optimized IR -> ...

# Components

## Front ends

- Clang
- Utrecht Haskell
- Glasgow Haskell Compiler

## Intermediate representation

IR is a strongly typed reduced instruction set computing (RISC)
instruction set which abstracts away details of the target.

## Back ends

The LLVM machine code (MC) sub-project is LLVM's framework for
translating machine instructions between textual forms and machine code.

## Linker

- The lld sub-project is an attempt to develop a built-in,
platform-independent linker for LLVM.
- Another linker: GNU ld

## C++ Standard Library

An implementation of the C++ Standard Library.

## Debugger

LLDB

# References

[wiki]: https://en.wikipedia.org/wiki/LLVM
