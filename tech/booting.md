[TOC]

# Overview
## The general meaning
- It gets the idea from "Bootstrapping process".
    + In general, bootstrapping usually refers to a self-starting
    process that is supposed to proceed without external input.
    + In computer technology the term (usually shortened to booting)
    usually refers to the process loading the basic software into the
    memory of a computer after power-on, especially the operating system
    kernel which will then take care of loading other software as
    needed.

## Software development
- A tiny assembler program was hand-coded for a new computer which
converted a few instructions into binary or decimal code (A1).
- This simple assembler program was then rewritten in its just-defined
assembly language but with extensions that would enable the use of some
additional mnemonics for more complex operation codes. The enhanced
assembler's source program was then assembled by its predecessor's
executable (A1) into binary or decimal code to give A2.

```
Human ------> First assembler ------> Second assembler ------> Repeated cycles ------> Final assembler
        ^         (A1)          ^           (A2)         ^            (An)       ^         (A*)
        |                       |                        |                       |
   Hand-coded               Assemble                 Assemble                 Assemble
```

### Compilers
- **A**: existed programming language
    + **C_A**: compiler of A
- **B**: new programming language
    + **C_B**: compiler of B

```
C_B code in A -----> temporary binary -----> final binary
                ^        C_B            ^        C_B
                |                       |
        compile by C_A        compile by temporary C_B
```

## History
- The ENIAC (1940s): doesn't need a boot process.
- The IBM 701 (1952-1956): punched card with initial program was used to
bootstrap the system.
- DEC PDP-8 (1965): using an array of switches.
- Integrated circuit Read-Only Memory (ROM) era (1975): Apple 1 (1976)
    + The ROM allows computers to be shipped with a start up program
    that could not be erased, and it uses to bootstrap the system.

# Booting
- Booting is a chain of events that starts with execution of
hardware-based procedures and may then hand-off to firmware and software
which is loaded into main memory.
    + Hard: after electrical power to the CPU is switched off to on.
    + Soft: power-on self-tests (POST) can be avoided.
- All computing systems are state machines, and a reboot may be the only
method to return to a designed zero-state from an unintended, locked
state.

## Booting sequences

### The summary table

```
| Power-on | Firmware (First stage bootloader) | Second stage bootloader        | Kernel           | initramfs                     | init                                 | getty                      | Display Manager | login                 | shell         | startx/xinit | Window Manager      | Apps     |
| -        | -                                 | -                              | -                | -                             | -                                    | -                          | -               | -                     | -             | -            | -                   | -        |
|          | (BIOS, UEFI, coreboot, libreboot) | (Syslinux, GRUB, bootx, ntldr) |                  |                               | systemd                              |                            | GNOME, KDE      |                       | zsh, bash     |              | i3, awesome, xmonad | chromium |
|          | POST process                      | kernel with parameters         | unpack initramfs | udev, lvm, encrypt            | call getty for each virtual terminal | ask username, password     | replace login   | create user's session | zshrc, bashrc | xinitrc      |                     |          |
|          | initializing peripheral devices   | load initramfs                 | `/init`          | mount real root               |                                      | call login/display manager |                 |                       |               |              |                     |          |
|          | load second stage bootloader      |                                | (kernel space)   | `/sbin/init` replaces `/init` |                                      |                            |                 |                       |               |              |                     |          |
|          |                                   |                                |                  | (early userspace)             |                                      |                            |                 |                       |               |              |                     |          |
```
