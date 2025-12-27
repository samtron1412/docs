[TOC]

# Overview

## The general meaning

- It gets the idea from "Bootstrapping process".
    + In general, bootstrapping usually refers to a self-starting
      process that is supposed to proceed without external input.
    + In computer technology the term (usually shortened to booting)
      usually refers to the process loading the basic software into the
      memory of a computer after power-on, especially the operating
      system kernel which will then take care of loading other software
      as needed.

## Software development

- A tiny assembler program was hand-coded for a new computer which
  converted a few instructions into binary or decimal code (A1).
- This simple assembler program was then rewritten in its just-defined
  assembly language but with extensions that would enable the use of
  some additional mnemonics for more complex operation codes. The
  enhanced assembler's source program was then assembled by its
  predecessor's executable (A1) into binary or decimal code to give A2.

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
  hardware-based procedures and may then hand-off to firmware and
  software which is loaded into main memory.
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


Power Button
    ↓
Firmware (BIOS/UEFI)
    ↓
Bootloader (GRUB/systemd-boot)
    ↓
Linux Kernel
    ↓
initramfs (early userspace)
    ↓
Init system (PID 1)
    ↓
Services / Login
    ↓
User session
```

### Steps

```
0. Power-on & Hardware Reset

Who: CPU + motherboard firmware
What happens:

Power button signals PSU

PSU stabilizes voltages

CPU resets to a known state

Instruction pointer jumps to firmware reset vector

➡️ Control passes to firmware

1. Firmware Phase (BIOS or UEFI)
1.1 POST (Power-On Self-Test)

Who: BIOS / UEFI
What happens:

Initialize CPU, RAM, chipset

Basic hardware checks

Detects storage devices

Initializes GPU for display output

1.2 Firmware Boot Selection
BIOS (Legacy)

Searches boot devices in order

Reads MBR (first 512 bytes) of boot disk

Jumps to bootloader code in MBR

UEFI

Loads UEFI boot manager

Reads EFI variables (NVRAM)

Loads .efi bootloader from ESP (EFI System Partition)

➡️ Control passes to bootloader

2. Bootloader Stage

Common bootloaders:

GRUB

systemd-boot

rEFInd

What happens:

Displays boot menu (optional)

Loads Linux kernel (vmlinuz)

Loads initramfs / initrd

Passes kernel command-line arguments

Transfers control to kernel

➡️ Bootloader exits forever

3. Linux Kernel Initialization

Who: Linux kernel
What happens:

Kernel decompresses itself

Initializes:

Memory management

Scheduler

Interrupts

CPU cores

Initializes essential drivers

Mounts initramfs as temporary root filesystem

➡️ Kernel starts PID 1

4. initramfs Stage (Early Userspace)

Who: initramfs (early userspace)
What happens:

Runs /init inside initramfs

Loads necessary drivers (storage, crypto, RAID)

Unlocks encrypted disks (LUKS)

Assembles RAID / LVM

Finds real root filesystem

Switches root (switch_root or pivot_root)

➡️ Control handed to real system

5. Init System (PID 1)

Common init systems:

systemd (most distros)

OpenRC

runit

s6

What happens:

PID 1 replaces initramfs init

Mounts filesystems (/, /home, /var)

Starts system services in dependency order

Sets hostname, time, locale

Starts login managers or getty

➡️ System becomes usable

6. User Space Startup
6.1 Console login

getty runs on TTYs

User logs in

Shell (bash, zsh) starts

6.2 Graphical login (optional)

Display manager starts:

GDM / SDDM / LightDM

Starts Wayland compositor or Xorg

Desktop environment / WM starts

7. User Session

What happens:

User environment loads

System ready for interaction

🎉 Boot completed
```

### Firmware - First stage bootloader

- Firmware: BIOS, UEFI, coreboot, libreboot
    + https://www.coreboot.org/
    + https://libreboot.org/
    + Flashing coreboot/libreboot firmware to ROM
        * https://forums.gentoo.org/viewtopic-p-8848270.html?sid=51809d833f8dcce8c3ed35f039c6cee3
        * https://forum.thinkpads.com/viewtopic.php?t=137498
- Functions:
    + Execute POSTs (power-on self-tests)
    + Initialize peripheral devices
    + Load second stage bootloader

#### POSTs

- A power-on self-test is a process that is performed by firmware or
  software routines immediately after an electronic device is powered
  on.
- The results of the POST may be displayed on a panel that is part of
  the device, output to an external device, or stored for future
  retrieval by a diagnostic tool.
- Since a POST might detect that the system's usual human-readable
  display is non-functional an indicator lamp or a speaker may be
  provided to show error codes as a sequence of flashes or beeps.
