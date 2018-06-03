[TOC]

# Overview

In computing, a **virtual machine** (VM) is an **emulation** of a
particular computer system. Virtual machines operate based on the
**computer architecture** and functions of a real or hypothetical
computer, and their implementations may involve specialized hardware,
software, or a combination of both.

# Classification

## System virtual machine

A **system virtual machine** provides a complete system platform which
supports the execution of a complete operating system (OS). These
usually **emulate an existing architecture**, and are built with the
purpose of either providing a platform to run programs where the real
hardware is not available for use (for example, executing on otherwise
obsolete platforms), or of having multiple instances of virtual machines
leading to more **efficient use of computing resources**, both in terms
of **energy consumption** and **cost effectiveness** (known as [hardware
virtualization](https://en.wikipedia.org/wiki/Hardware_virtualization),
the key to a cloud computing environment), or both.

### Advantages

- Multiple OS environment, sharing files.
- Application provisioning, maintenance, high availability and disaster
  recovery
- Multiple instruction set architecture (ISA)

### Disadvantage

- Less efficitent than actual machine
- Unstable performance

## Process virtual machine

A process virtual machine (also, **language virtual machine**) is
designed to run a single program, which means that it supports a single
process. Such virtual machines are usually closely suited to one or more
programming languages and built with the purpose of providing program
**portability** and **flexibility** (amongst other things). An essential
characteristic of a virtual machine is that the software running inside
is limited to the resources and abstractions provided by the virtual
machine—it cannot break out of its virtual environment.

# Techniques

## Virtualization of the underlying raw hardware (native execution)

[Hardware-assisted virtualization](https://en.wikipedia.org/wiki/Hardware-assisted_virtualization)

This approach is full virtualization of the hardware, and can be
implemented using a Type 1 or Type 2
[hypervisor](https://en.wikipedia.org/wiki/Hypervisor)

The standard **x86 processor architecture** as used in the modern PCs
does not actually meet the [Popek and Goldberg virtualization requiremen
ts](https://en.wikipedia.org/wiki/Popek_and_Goldberg_virtualization_requ
irements). Notably, there is no **execution mode** where all sensitive
machine instructions always trap, which would allow **per-instruction
virtualization**.

Intel and AMD have introduced features to their x86 processors to enable
[virtualization in hardware](https://en.wikipedia.org/wiki/Hardware-
assisted_virtualization).


## Emulation of a non-native system



## Operating system - level virtualization


