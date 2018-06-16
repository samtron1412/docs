[TOC]

# Overview

Device-mapper is infrastructure in the Linux 2.6 and 3.x kernel that
provides a generic way to create virtual layers of block devices.

- Device-mapper crypt target provides transparent encryption of block
  devices using the kernel crypto API.
    + user specify one of the symmetric ciphers, an encryption mode, a
      key, an iv generation mode and then the user can crate a new block
      device in /dev.
    + you can mount your filesystem on it as usual or stack dm-crypt
      device with another device like RAID or LVM volume

# Common scenarios

## Encrypting entire system

### Overview

- simple partition layout with LUKS
    + simple partitioning and setup
    + inflexible; dis-space to be encrypted has to be pre-allocated
- LVM on LUKS
    + using LVM inside a single LUKS encrypted partition
    + advantages
        * easiest method to allow suspension to disk
        * only one key required
        * volume layout not transparent when locked
    + disadvantages
        * LVM adds an additional mapping layer and hook
        * less useful, if a singular volume should receive a separate
          key
- LUKS on LVM
    + dm-crypt only after the LVM is setup
    + advantages
        * LVM can be used to have encrypted volumes span multiples disks
        * easy mix of un-/encrypted volume groups
    + disadvantages
        * complex; changing volumes requires changing encryption mappers
          too
        * Volumes require individual keys
        * LVM layout is transparent when locked
- LUKS on software RAID
    + dm-crypt only after RAID is setup
    + advantage
        * analogous to LUKS on LVM
    + disadvantages
        * analogous to LUKS on LVM
- Plain dm-crypt
    + without a LUKS header and its options for multiple keys
    + advantages
        * data resilience for cases where a LUKS header may be damaged
        * full disk encryption
        * addressing problems with SSDs
    + disadvantages
        * high care to all encryption parameters is required
        * single encryption key and no option to change it
- encrypted boot partition with GRUB
- btrfs subvolumes with swap


### LVM on LUKS

```
+-----------------------------------------------------------------------+ +----------------+
| Logical volume 1      | Logical volume 2      | Logical volume 3      | | Boot partition |
|                       |                       |                       | |                |
| [SWAP]                | /                     | /home                 | | /boot          |
|                       |                       |                       | |                |
| /dev/MyVolGroup/swap  | /dev/MyVolGroup/root  | /dev/MyVolGroup/home  | |                |
|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _| | (may be on     |
|                                                                       | | other device)  |
|                         LUKS encrypted partition                      | |                |
|                           /dev/sda1                                   | | /dev/sdb1      |
+-----------------------------------------------------------------------+ +----------------+
```

# Drive preparation

## Securely erasing the drive

Something

## Partitioning

### Introduction

Almost every case these has to be a separate partition for `/boot` that
must remain unencrypted, because the bootloader needs to access the
`/boot` directory where it will load the initramfs/encryption modules
needed to load the rest of the system.

### Physical partitions

- Similar to an unencrypted system
- Separate passphrase or keys are required to open each encrypted
  partition
    + can be automated during boot using the crypttab

### Stacked block devices

- coexist with LVM or RAID
- If LVM/RAID devices are on top of dm-crypt
    + possible to add, remove and resize the file systems of the same
      encrypted partition
    + only one key or passphrase will be required
    + not be possible to span multiple disks
- If the encrypted layer is on top of LVM/RAID
    + still can be possible to reorganize the file systems in the
      future, but with added complexity, since the encryption layers
      will have to be adjusted accordingly
    + separate passphrases or keys will be required to open each
      encrypted device
    + the only option for a system to span on multiple disks

### Btrfs subvolumes

- Btrfs's subvolumes feature can be used as LVM
    + Not supported swap partition => an encrypted swap partition is
      needed

# Device encryption

Covers how to manually utilize dm-crypt to encrypt a system through the
cryptsetup command.

- Encryption options with dm-crypt
- the creation of keyfiles
- LUKS specific commands for key management
- backup and restore

# System configuration

Illustrates how to configure `mkinitcpio`, the boot loader and the
crypttab file when encrypting a system.

## mkinitcpio

Something

## Boot loader

Something

## crypttab

Something

# Swap device encryption

Without or with suspend-to-disk support

## Without suspend-to-disk support

Something

## With suspend-to-disk support

Something

# Specialties

- Securing the unencrypted boot partition
- Using GPG or OpenSSL encrypted keyfiles
- boot and unlock via the network
- setting up discard/TRIM for a SSD
- dealing with the encrypt hook and multiple disks

## Discard/TRIM support for a SSD

- http://asalor.blogspot.com/2011/08/trim-dm-crypt-problems.html

# References

[awiki]: https://wiki.archlinux.org/index.php/Dm-crypt
