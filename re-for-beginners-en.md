[TOC]

# Acronyms
- PL: Programming Language
- PRNG: PseudoRandom Number Generator
- RA: Return Address
- PE: Portable Executable
- SP: Stack Pointer. SP/ESP/RSP in x86/x64. SP in ARM
- DLL: Dynamic Link Library
- PC: Program Counter. IP/EIP/RIP in x86/x64. PC in ARM
- LR: Link Register
- IDA: Interactive DisAssembler
- VA: Virtual Address
- OEP: Original Entry Point
- MSVC: MicroSoft Visual C++
- MSVS: MicroSoft Visual Studio
- ASLR: Address Space Layout Randomization
- MFC: Microsoft Foundation Classes
- AKA: Also Known As
- CRT: C Runtime Library
- CPU: Central Processing Unit
- FPU: Floating Point Unit
- CISC: Complex Instruction Set Computing
- RISC: Reduced Instruction Set Computing
- GUI: Graphical User Interface
- SIMD: Single Instruction, Multiple Data
- DBMS: DataBase Management System
- ISA: Instruction Set Architecture
- CGI: Common Gateway Interface
- HPC: High Performance Computing
- SOC: System On Chip
- ELF: Executable file format widely used in *NIX system include Linux
- NAN: Not A Number
- NOP: No Operation
- BEQ: Branch if Equal
- BNE: Branch if Not Equal
- BLR: Branch to Link Register
- XOR: eXclusive OR
- MCU: Micro Controller Unit
- RAM: Random Access Memory
- ROM: Read Only Memory
- VGA: Video Graphic Array
- API: Application Programming Interface
- ASCII: American Standard Code for Information Interchange
- ASCIIZ: ASCII Zero (null-terminated ASCII string)
- IA64: Intel Architecture 64 (Itanium)
- MSDN: MicroSoft Developer Network
- MSB: Most Significant Bit/Byte
- STL (C++) Standard Template Library
- HDD: Hard Disk Drive
- VM: Virtual Memory
- GPR: General Purpose Registers
- RE: Reverse Engineering
- BCD: Binary Coded Decimal
- GDB: GNU Debugger
- 

# Glossary
- Tail call: It is when compiler (or interpreter) transforms recursion (with which it is possible: tail recursion) into iteration for efficiency: [link](http://en.wikipedia.org/wiki/Tail_call. 13)
- callee: a function being called by another.
- caller: a function calling another.
- compiler intrinsic:  A function specific to a compiler which is not usual library function. Compiler generate a specific machine code instead of call to it. It is often a pseudofunction for specific CPU instruction.
- CP/M: Control Program for Microcomputers: a very basic disk OS used before MS-DOS
- debuggee: a program being debugged
- dongle: Dongle is a small piece of hardware connected to LPT printer port (in past) or to USB. Its function was akin to security token, it has some memory and, sometimes, secret (crypto-)hashing algorithm
- endianness: byte order
- leaf function: a function which is not calling any other function
- link register: (RISC) A register where return address is usually stored. This makes calling leaf functions without stack usage, i.e., faster..
- Windows NT: Windows NT, 2000, XP, Vista, 7, 8
- xoring: applying XOR operation
- name mangling: (also called `name decoration`) is a technique used to solve various problems caused by the need to resolve unique names for programming entities in many modern programming languages. It provides a way of encoding additional information in the name of a **function, structure, class** or another datatype in order to pass more semantic information from the compilers to **linkers**.

# Tools
## Disassembler
- IDA: cross-platform
- OllyDbg: user-mode Win32

## Debugger
- GDB: GNU Debugger

## Decompiler
- Hex-Rays

## Other
- Hiew: binary editor
- Microsoft Visual Studio Express

# Worth reading
## Book
- Windows: Windows Internal, Mark E. Russinovich and David A. Solomon with Alex Ionescu
- C/C++
- x86/x86-64
- ARM

## [Stack Exchange](http://reverseengineering.stackexchange.com/)



# Fundamentals
## Signed number representations
There are several methods of representing signed number, but in x86 architecture used "two's complement".
<figure>
  <figcaption style="text-align:center;">Two Complement</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="RE_beginer_Figures/twocomplement.png" alt="Two Complement" title="Two Complement">
</figure>

### Integer overflow

## Endianness
Endianness is a way of representing values in memory.
### Big-endian
Value 0x12345678 will be presented in memory: 0x12 0x34 0x56 0x78. Motorola 68k, IBM POWER.

### Little-endian
Value 0x12345678 will be presented in memory: 0x78 0x56 0x34 0x12. Intel x86.

### Bi-endian
CPUs which may switch between endianness: ARM, PowerPC, SPARC, MIPS, IA64, etc.
# Finding important/interesting stuff in the code
One of the primary reverse engineer’s task is to find quickly in the code what is needed.

`IDA` disassembler allow us search among text strings, byte sequences, constants. It is even possible to export the code
into `.lst` or `.asm` text file and then use `grep, awk, etc.`

When you try to understand what a code is doing, this easily could be some open-source library like libpng. So when you see some constants or text strings looks familiar, it is always worth to google it. And if you find the open-source project where it is used, then it will be enough just to compare the functions. It may solve some part of problem.

For example, if program use a XML files, the first step may be determining, which XML-library is used for processing, since
standard (or well-known) library is usually used instead of self-made one.

## Identification of executable files
### Microsoft Visual C++
MSVC versions and DLLs which may be imported. msvcp*.dll contain C++-related functions, so, if it is imported, this is probably C++ program.

<figure>
  <figcaption style="text-align:center;">MSVC versions</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="RE_beginer_Figures/msvcversion.png" alt="MSVC versions" title="MSVC versions">
</figure>

Name mangling: Names are usually started with `?` symbol.

### GCC
Aside from *NIX targets, GCC is also present in win32 environment: in form of Cygwin and MinGW.

Name mangling: Names are usually started with `_Z` symbols.

Cygwin: `cygwin1.dll` is often imported.

MinGW: `msvcrt.dll` may be imported.

## Communication with the outer world (win32)
