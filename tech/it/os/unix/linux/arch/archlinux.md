[TOC]

# Overview

Arch Linux, a lightweight and flexible Linux distribution that tries to
Keep It Simple.

Arch Linux is an independently developed, **i686/x86-64** general
purpose GNU/Linux distribution versatile enough to suit any role.
Development focuses on **simplicity**, **minimalism**, and **code
elegance**. Arch is installed as a minimal base system, configured by
the user upon which their own ideal environment is assembled by
installing only **what is required or desired for their unique
purposes**. GUI configuration utilities are not officially provided, and
most system **configuration is performed from the shell by editing
simple text files**.

## The Arch Way

The acronym KISS for **Keep It Simple, Stupid**.

### Simplicity

Arch Linux defines simplicity as **without unnecessary additions,
modifications, or complications**, and provides a **lightweight UNIX-
like base structure** that allows an individual user to shape the system
according to their own needs.

### Code-correctness over convenience

The Arch Linux system places precedence upon elegance of design as well
as **clean, correct, simple code**, rather than unnecessary patching,
automation, eye candy or "newbie-friendliness." Software patches are
therefore kept to an absolute minimum; ideally, never. Simple design and
implementation shall always trump simple user interface.

Simplicity of implementation, code-elegance, and minimalism shall always
remain the reigning priorities of Arch development.

### User-centric vs User-friendly

Arch Linux targets and accommodates competent GNU/Linux users by giving
them **complete control and responsibility over the system**.

"do-it-yourself" approach. "do first, then ask" philosophy

### Openness

live, active communities

### Freedom

Provides the freedom to make any choice about the system.

## History

Arch Linux was founded by Canadian programmer Judd Vinet. Its first
formal release, Arch Linux 0.1, was on March 11, 2002. In 2007, Judd
Vinet stepped down as Project Lead to pursue other interests and was
replaced by American programmer Aaron Griffin who continues to lead the
project today.

## Modernity

Arch Linux uses a rolling release system which allows one-time
installation and perpetual software upgrades. It is not generally
necessary to reinstall or upgrade your Arch Linux system from one
"version" to the next. By issuing one command, an Arch system is kept
up-to-date and on the bleeding edge.

Use systemd init system, modern **filesystems (Ext2/3/4, Reiser, XFS,
JFS, BTRFS)**, **LVM2**, **software RAID**, **udev** support and
**initcpio** (with mkinitcpio), as well as the latest available kernels.

## Software packaging

Arch Linux uses its own `Pacman` package manager, which couples simple
binary packages with an easy-to-use package build system. This allows
users to easily manage and customize packages ranging from official Arch
software to the user's own personal packages to packages from 3rd party
sources. The repository system also allows users to easily build and
maintain their own custom build scripts, packages, and repositories,
encouraging community growth and contribution.

Currently we have *official packages* optimized for the i686 and x86-64
architectures. We complement our official package sets with a
*community- operated package repository* (AUR), which contains many
thousands of user-maintained **PKGBUILD** scripts for compiling
installable packages from source using the **makepkg** application. It
is also possible for users to easily build and maintain their own custom
repositories..

# Community

- [wiki][awiki]
- [forums][forums]
- [bugs][bugs]
- [mailing lists][mailing-lists]
- [irc][irc]
- [international communities][international]
- [Getting involved][involve]

## Help

### Reading

#### Regular user or root

The numeral or hash sign `#` indicates that the line is to be entered as
**root**. Whereas the dollar sign `$` show that the line is to be
entered as **a regular user**.

    # mkinitcpio -p linux
    $ makepkg -s

#### Installation of packages

Official packages: `# pacman -S <package>`

Arch User Repository
1. Download tarball
2. Extract the tarball: `tar xzf foobar.tar.gz`
3. Run `makepkg` (`makepkg -s` will automatically resolve dependencies
   with pacman). This will download the code, compile it and pack it.
4. Look for a README file in `src/`, contain some useful information.
5. Install with pacman: `# pacman -U /path/to/pkg.tar.xz`

These manually installed packages are called foreign packages — packages
which have not originated from any repository known to pacman. To list
all foreign packages: `$ pacman -Qm`

#### Control of systemd units

Start service: `systemctl start example.service`

Enable service: `systemctl enable example.service`

### Style


# Pre-Installation

## Securely wipe disk

Something

## Disk Encryption

### Resources

- http://tech.memoryimprintstudio.com/dual-boot-installation-of-arch-linux-with-preinstalled-windows-10-with-encryption/
- https://wiki.archlinux.org/index.php/Dm-crypt/Encrypting_an_entire_system

### Introduction

Cryptographically protecting a logical part of a storage disk (folder,
partition, whole disk, ...)

- Storage disks
    + computer's hard drive(s)
    + external devices
        * USB, DVD
    + virtual storage disks (as long as Arch Linux can address it as a
      block device or filesystem)
        * loop-back devices, cloud storage

### Why use encryption?

Disk encryption ensures that files are always stored on disk in an
encrypted form. The files only become available to the operating system
and applications in readable form while the system is running and
unlocked by a trusted user. An unauthorized person looking at the disk
contents directly, will only find garbled random-looking data instead of
the actual files.

You will still be vulnerable to:

- Attackers who can break into your system (e.g. over the Internet)
  while it is running and after you have already unlocked and mounted
  the encrypted parts of the disk.
- Attackers who are able to gain physical access to the computer while
  it is running, or very shortly after it was running, if they have the
  resources to perform a *cold boot attack*.
- A government entity, which not only has the resources to easily pull
  off the above attacks, but also may simply force you to give up your
  keys/passphrases using various techniques of *coercion*.
    + In most non-democratic countries around the world, as well as in
      the USA and UK, it may be legal for law enforcement agencies to do
      so if they have suspicions that you might be hiding something of
      interest.

Strong disk encryption setup:

- Full system encryption with authenticity checking and no plaintext
  boot partition
- Hardware-based full disk encryption
    + https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption
- Trusted Computing
    + https://en.wikipedia.org/wiki/Trusted_Computing

### Data encryption vs system encryption

Data encryption

- Only the user's data (/home, or removable media)
- Background processes that may cache/store information about user data
  or parts of the data itself in non-encrypted areas
    + swap partitions
    + /tmp
    + /var
- vulnerable to offline system tampering attacks
    + someone installing a hidden program that records the passphrase
      you use to unlock the encrypted data, or waits for you to unlock
      it and then secretly copies/sends some of the data to a location
      where the attacker can retrieve it.

System encryption

- the encryption of the operating system and user data
- an adjunct to the existing security mechanisms
    + securing offline physical access
    + network security
    + user-based access control

### Available methods

All disk encryption methods operate in such a way that even though the
disk actually holds encrypted data, the operating system and
applications "see" it as the corresponding normal readable data as long
as the cryptographic container (i.e. the logical part of the disk that
holds the encrypted data) has been "unlocked" and *mounted*.

For this to happen, some "*secret information*" (usually in the form of
a keyfile and/or passphrase) needs to be supplied by the user, from
which the *actual encryption key* can be derived (and stored in the
kernel keyring for the duration of the session).

Two types by their layer of operation:

- Stacked filesystem encryption
    + stacks on top of an existing filesystem
        * all files written to an encryption-enabled folder to be
          encrypted on-the-fly before the underlying filesystem writes
          them to disk
        * and decrypted whenever the filesystem reads them from disk
    + *eCryptfs*, *EncFS*
    + Cloud-storage optimized: *gocryptfs*, *cryptomator*, *cryfs*
- Block device encryption
    + operate below the filesystem layer and make sure that everything
      written to a certain block device (i.e. a whole disk, or a
      partition, or a file acting as a virtual loop-back device) is
      encrypted.
    + *loop-AES*
        * a descendant of cryptoloop and is a secure and fast solution
        * less user-friendly than other options as it requires non-
          standard kernel support
    + *dm-crypt*
        * the standard device-mapper encryption functionality provided
          by the Linux kernel.
        * types of block-device encryption: LUKS (default), plain,
          limited features for loopAES and Truecrypt devices.
        * *LUKS*, used by default, is an additional convenience layer
          which stores all of the needed setup information for dm-crypt
          on the disk itself and abstracts partition and key management
          in a n attempt to improve ease of use and cryptographic
          security.
        * *plain* dm-crypt mode, being the original kernel
          functionality, does not employ the convenience layer. It is
          more difficult to apply the same cryptographic strength with
          it.When doing so, longer keys (passphrases or keyfiles) are
          the result.
    + *TrueCrypt*/*VeraCrypt*
        * TrueCrypt was discontinued in May 2014
        * VeraCrypt fork was audited in 2016

### Preparation

#### Choosing a setup

- System encryption
    + block device
- Passphrase to unlock
- Unlock during boot

#### Choosing a strong passphrase

#### Preparing the disk

- Securely wiping it first
    + overwriting the entire drive or partition with a stream of zero
      bytes or random bytes
    + zero bytes will be much faster
    + high-quality random bytes can hide the usage patterns

### How the encryption works?

#### Basic principle

```
          ╔═══════╗
 sector 1 ║"???.."║
          ╠═══════╣         ╭┈┈┈┈┈╮
 sector 2 ║"???.."║         ┊ key ┊
          ╠═══════╣         ╰┈┈┬┈┈╯
          :       :            │
          ╠═══════╣            ▼             ┣┉┉┉┉┉┉┉┫
 sector n ║"???.."║━━━━━━━(decryption)━━━━━━▶┋"abc.."┋ sector n
          ╠═══════╣                          ┣┉┉┉┉┉┉┉┫
          :       :
          ╚═══════╝

          encrypted                          unencrypted
     blockdevice or                          data in RAM
       file on disk
```

Whenever the encrypted block device or folder is to be mounted, its
corresponding key (master key) must be supplied.

Two techniques to increase the quality of keys:

- Using cryptography to increase the entropic property of the master key
  based on a separate human-friendly passphrase
- Create a keyfile with high entropy and store it on a medium separate
  from the data drive to be encrypted.

#### Cryptographic metadata

```
╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮                         ╭┈┈┈┈┈┈┈┈┈┈┈╮
┊ mount passphrase ┊━━━━━⎛key derivation⎞━━━▶┊ mount key ┊
╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ,───⎝   function   ⎠    ╰┈┈┈┈┈┬┈┈┈┈┈╯
╭──────╮            ╱                              │
│ salt │───────────´                               │
╰──────╯                                           │
╭─────────────────────╮                            ▼         ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
│ encrypted master key│━━━━━━━━━━━━━━━━━━━━━━(decryption)━━━▶┊ master key ┊
╰─────────────────────╯                                      ╰┈┈┈┈┈┈┈┈┈┈┈┈╯
```

The key derivation function (e.g. PBKDF2 or scrypt) is deliberately slow
=> no brute-force attacks

- salt: randomly generated
- encrypted master key can be stored on disk together with the encrypted
  data => the confidentiality of the encrypted data depends completely
  on the secret passphrase.
- storing the encrypted master key in a keyfile instead of storing with
  the encrypted data => two-factor authentication
    + something only you know: passphrase
    + something only you have: keyfile

After we have the master key:

```
                          ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
                          ┊ master key ┊
  file on disk:           ╰┈┈┈┈┈┬┈┈┈┈┈┈╯
 ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐        │
 ╎╭───────────────────╮╎        ▼          ╭┈┈┈┈┈┈┈┈┈┈╮
 ╎│ encrypted file key│━━━━(decryption)━━━▶┊ file key ┊
 ╎╰───────────────────╯╎                   ╰┈┈┈┈┬┈┈┈┈┈╯
 ╎┌───────────────────┐╎                        ▼           ┌┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┐
 ╎│ encrypted file    │◀━━━━━━━━━━━━━━━━━(de/encryption)━━━▶┊ readable file ┊
 ╎│ contents          │╎                                    ┊ contents      ┊
 ╎└───────────────────┘╎                                    └┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┘
 └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
```

#### Ciphers and modes of operation

Ciphers: the actual algorithm used for translating between pieces of
unencrypted and encrypted data (plaintext and ciphertext)

- AES
- Blowfish
- Twofish
- Serpent

Modes of operation: a set of rules for how to consecutively apply the
cipher to the individual blocks

- electronic codebook (ECB) mode: applying it to each block separately
  without modification
    + recognize patterns
- cipher-block chaining (CBC) mode: each block of plaintext data is
  combine in a mathematical way with the ciphertext of the previous
  block, before encrypting it using the cipher.
    + first block needs *initialization vector (IV)* => needs a way to
      securely generate IV

```
                                  ╭──────────────╮
                                  │initialization│
                                  │vector        │
                                  ╰────────┬─────╯
          ╭  ╠══════════╣        ╭─key     │      ┣┉┉┉┉┉┉┉┉┉┉┫
          │  ║          ║        ▼         ▼      ┋          ┋         . START
          ┴  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"Hello, W"┋ block  ╱╰────┐
    sector n ║          ║                         ┋          ┋ 1      ╲╭────┘
  of file or ║          ║──────────────────╮      ┋          ┋         '
 blockdevice ╟──────────╢        ╭─key     │      ┠┈┈┈┈┈┈┈┈┈┈┨
          ┬  ║          ║        ▼         ▼      ┋          ┋
          │  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"orld !!!"┋ block
          │  ║          ║                         ┋          ┋ 2
          │  ║          ║──────────────────╮      ┋          ┋
          │  ╟──────────╢                  │      ┠┈┈┈┈┈┈┈┈┈┈┨
          │  ║          ║                  ▼      ┋          ┋
          :  :   ...    :        ...      ...     :   ...    : ...

               ciphertext                         plaintext
                  on disk                         in RAM
```

# [Installation][installation]

## Preparation

A working Internet connection is required.

### System requirements

Run on any i686 compatible machine with a minimum of 64 MB RAM. A basic
installation with all packages from the [base][base] group should take
less than 800 MB of disk space.

### Prepare the latest installation medium

The latest release of the installation media can be obtained from the
[Download][download] page. Burn the ISO image on a CD/DVD/USB.

## Boot the installation medium

You are now presented with a shell prompt, automatically logged in as
root.

## Change the language

- Load keyboard: **loadkeys us** (default is us, so didn't change)
- Set font: **setfont Lat2-Terminus16**
    + List all font are installed: **$ fc-list**
    + Search font available: **$ pacman -Ss font**
    + Search font ttf: **$ pacman -Ss ttf**
    + Make package font from TTFs use *makefontpkg* from the AUR
- Change language if don't want US: **nano /etc/locale.gen**

## Prepare the storage devices

Partitioning will destroy existing data. Before proceeding, you **must**
backup all data.

Users intending to create stacked block devices for [LVM][lvm], disk
[encryption][encryption] or [RAID][raid], should keep those instructions
into consideration when preparing the partitions.

### Identify the devices

Show all the available devices: `# lsblk`

Devices (e.g. hard disks) will be listed as `sdx`, where `x` is a lower-
case letter starting from a for the first device (`sda`), b for the
second device (`sdb`), and so on. Existing partitions on those devices
will be listed as `sdxY`, where `Y` is a number starting from `1` for
the first partition, `2` for the second, and so on. In the example
below, only one device is available (`sda`), and that device uses only
one partition (`sda1`):

    NAME            MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda               8:0    0    80G  0 disk
    └─sda1            8:1    0    80G  0 part

### Partition table types

Choose the partition table type: GPT (GUID Partition Table) for UEFI
boot and MBR (Master Boot Record) for BIOS boot.

There are two types of partition table:
- MBR: Intended for BIOS systems (also referred to as "msdos")
- GPT: Intended for UEFI systems

Any existing partition table can be identified with the following
command for each device: `# parted /dev/sdx print`

### Partitioning tools

- Beginner: [GParted][gparted]
- *gdisk* recommend for GPT
- *fdisk* recommend for MBR
- *parted* for MBR and GPT

With MBR type, we only can four primary partitions. To create more than
four partitions, we will create three primary partition and one extended
partition (maybe one primary and one extended, etc.), in extended
partition we can create more logical partition.

It mean extended partition is a container can contain more logical
partition.

Different between primary and logical partition is only some operating
system can not boot from logical partition. (like Windows OS)

### Create new partition table

Partition scheme:

| Partition | Description                                                                                                                                                                               |
| -         | -                                                                                                                                                                                         |
| `/`       | root directory, must be mounted first, directories essential like `/etc` or `/usr` must be on the same partition as `/` or mounted in early userspace by the `initramfs`, capacity 30 GB. |
| `/boot`   | contains the kernel, ramdisk images and bootloader configuration file and boot loader stages, 200 - 300 MB                                                                                |
| `/home`   | contains user-specific configuration files, caches, application data and media files, capacity = 3/4 of total capacity                                                                    |
| `swap`    | virtual memory, capacity = 3/2 of RAM memory (using hibernate)                                                                                                                            |
| `/var`    | stores variable data such as spool directories and files, administrative and logging data, pacman's cache, the ABS tree, etc. 30 GB                                                       |
| `/tmp`    | This is already a separate partition by default, by being mounted as `tmpfs` by systemd.                                                                                                  |

Use **lsblk** to list the hard disks

### Create filesystem

    # mkfs.ext4 /dev/sda1
    # mkfs.ext4 /dev/sda2

### Activate swap

    # mkswap /dev/sdaX
    # swapon /dev/sdaX

### Mount the partitions

- Dislay current layout of disk: `# lsblk -f`
- Mount `/` to `/mnt`: `# mount /dev/sda1 /mnt`
- Mount `/home`, `/boot`:
        # mkdir /mnt/home
        # mount /dev/sda2 /mnt/home

## Establish an Internet connection

- **dhcpcd** is auto run during boot and start a wired connection ->
  check:
    + `$ ping www.google.com`

### Wireless

- Identify the name of your wireless interface: `# iw dev`
- Connect to a network: `# wifi-menu <name of wireless interface>`
- Without wifi-menu:
    + List interface: `# ip link`
    + Bring the interface up: `# ip link set <interface> up`
    + Verify: `# ip link show <interface>`
    + Scan available network: `# iw dev <interface> scan | grep SSID`
    + Connect to a network: `# wpa_supplicant -B -i <interface> -c <(wpa_passphrase "<ssid>" "<password>")`
    + Set IP: `# dhcpcd <interface>`

## Select a mirror

    # vi /etc/pacman.d/mirrorlist

- Choose line, cut line, go to top, paste it.
- HTTP faster than FTP
- After change mirror in the future, refresh all packages list with
  **pacman -Syy**.

### Select the fastest mirror

Back up mirror:
- `# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup`
- Generate mirrors list follow [status of mirrors][mirrors].
- Save it to `/etc/pacman.d/mirrorlist.new`.
-  Check [online mirrors status][mirror- status].

Edit `mirrorlist.new` and uncomment mirrors for testing:
- `# sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.new`

Run this command
- `# rankmirrors -n 6 /etc/pacman.d/mirrorlist.new > /etc/pacman.d/mirrorlist`

## Install the base system

    # pacstrap -i /mnt base base-devel

## Generate an fstab

    # genfstab -U -p /mnt >> /mnt/etc/fstab

    # vi /mnt/etc/fstab

> The `fstab` file should always be checked after generating it. If you
> encounter errors running genfstab or later in the install process, do
> not run genfstab again; just edit the `fstab` file. See [fstab#Field d
> efinitions](https://wiki.archlinux.org/index.php/Fstab#Field_definitio
> ns) for syntax information.

=> edit file fstab: last field determine the order in which partitions
are checked at start up, 1 for root partition, 2 for orther you want
check, 0 mean do not check ( swap partition)

## Change root and configure the base system

    # arch-chroot /mnt /bin/bash

Leave out /bin/bash to chroot into the **sh** shell.

At this stage of the installation, you will configure the primary
configuration files of your Arch Linux base system. These can either be
created if they do not exist, or edited if you wish to change the
defaults.

### locale

Locales are used by glibc and other locale-aware programs or libraries
for rendering text, correctly displaying regional monetary values, time
and date formats, alphabetic idiosyncrasies, and other locale-specific
standards. There are two files that need editing: **locale.gen** and
**locale.conf**.

    # vi /etc/locale.gen -> remove # before language you choose

Generate the locale(s) specified in /etc/locale.gen:

    # locale-gen

Create the /etc/locale.conf file substituting your chosen locale:

    # echo LANG=en_US.UTF-8 > /etc/locale.conf

Export substituting your chosen locale:

    # export LANG=en_US.UTF-8

### console font and keymap (only when changed default)

-> **if you changed default console keymap and font**, create
vconsole.conf if does not exist:

    # vi /etc/vconsole.conf

KEYMAP=us
FONT=ter-116n

### time zone:

    # ln -s /usr/share/zoneinfo/<Zone>/<SubZone> /etc/localtime

### hardware clock

    # hwclock --systohc --utc

Force Windows use UTC, search Google:
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
     "RealTimeIsUniversal"=dword:00000001
- disable windows time service: **sc config w32time start= disabled**
- enable window time service: **sc config w32time start= demand**

### hostname:

    # echo myhostname > /etc/hostname

### configure the network

Use `netctl` to create a profile and start it.

Copy and edit example profiles in `/etc/netctl/examples/` to
`/etc/netctl/` after that list profile with command: `# netctl list`

Start a profile: `# netctl start <profile>`

Enable a profile: `# netctl enable <profile>`

#### Wireless

    # pacman -S dialog

    # wifi-menu <interface>

Connect automatically to known networks

    # pacman -S wpa_actiond

    # systemctl enable netctl-auto@interface_name.service

### set passwd

    # passwd

### Initramfs

Creating a new initramfs is usually not required, because mkinitcpio was
run on installation of the linux package with **pacstrap**.

For special configurations, modify the mkinitcpio.conf(5) file and
recreate the initramfs image:

    # mkinitcpio -p linux

### Install and configure a boot loader

#### Syslinux

Install the **syslinux** package and then use the **syslinux-
install_update** script to automatically install the bootloader
(**-i**), mark the partition active by setting the boot flag (**-a**),
and install the MBR boot code (**-m**):

    # pacman -S syslinux
    # syslinux-install_update -iam

After installing Syslinux, configure `syslinux.cfg` to point to the
right root partition. This step is vital (important). If it points to
the wrong partition, Arch Linux will not boot. Change **/dev/sda3** to
reflect your root partition

    # nano /boot/syslinux/syslinux.cfg
    ...
    LABEL arch
            ...
            APPEND root=/dev/sda3 rw
            ...

If adding UUID rather than partition number the syntax is
**APPEND root=UUID=partition_uuid rw**.

#### GRUB

Install grub packet: `# pacman -S grub`
- `# grub-install --target=i386-pc --recheck /dev/sda`

Install os-prober: `# pacman -S os-prober`
- `# grub-mkconfig -o /boot/grub/grub.cfg`


## Unmount and reboot

    # exit
    # umount -R /mnt
    # reboot


# [Post Installation][post-installation]

## 1. System administration

This section deals with administration task and system management.

### 1.1. Users and Groups management

#### Why?

Logging in as root for prolonged periods of time, possibly even exposing
it via SSH on a server, is in secure.

#### What?

You should create and use unprivileged user account(s) for most tasks,
only using the root account for system administration.

Users and groups are a mechanism for **access control**.

- **A User** is anyone who uses a computer. We are describing the names
  which represent those users. Each account has a name.
- **Managing users** is done for the purpose of security by limiting
  access in certain specific ways.
- **The superuser** (root) has complete access to the operating system
  and its configuration.
- **Unprivileged users** can use the `su` and `sudo` programs for
  controlled privilege escalation.

##### Permissions and ownership


#### How?

##### User management

- Create two users: `glider` with password and `guest` with no password
- List users logged on system: `$ who`
- Add a new user:
    + `$ useradd -m -g [initial_group] -G [additional_group] -s [login_shell] [username]`
    + `# useradd -m -G wheel -s /bin/bash glider`
    + `# useradd -m -s /bin/bash guest`
- Del a user: `$ userdel -r [username]`
- Specify the user's password: `$ passwd [username]`
    + `# passwd glider`
- User database: `$ cat /etc/passwd`
- Shadow file: `$ cat /etc/shadow`

##### Group management

- List of groups and users belong group: `$ cat /etc/group`
- Create a new group: `$ groupadd [group]`
- Add users to a group: `$ gpasswd -a [user] [group]`
- Remove users from a group: `$ gpasswd -d [user] [group]`
- Del a existing group: `$ groupdel [group]`

### 1.2. Privilege escalation

### 1.3. Service management

+ list all units of system: $ systemctl
+ list all failed units: $ systemctl --failed
Activate a unit immediately:
    # systemctl start unit
Deactivate a unit immediately:
    # systemctl stop unit
Restart a unit:
    # systemctl restart unit
Ask a unit to reload its configuration:
    # systemctl reload unit
Show the status of a unit, including whether it is running or not:
    $ systemctl status unit
Check whether a unit is already enabled or not:
    $ systemctl is-enabled unit
Enable a unit to be started on bootup:
    # systemctl enable unit
Disable a unit to not start during bootup:
    # systemctl disable unit
Show the manual page associated with a unit (this has to be supported by the unit file):
    $ systemctl help unit
Reload systemd, scanning for new or changed units:
    # systemctl daemon-reload

- Power management:
    Shut down and reboot the system:
        $ systemctl reboot
    Shut down and power-off the system:
        $ systemctl poweroff
    Suspend the system:
        $ systemctl suspend
    Put the system into hibernation:
        $ systemctl hibernate
    Put the system into hybrid-sleep state (or suspend-to-both):
        $ systemctl hybrid-sleep

- Sound:
    + Install alsa-utils: $ pacman -S alsa-utils
    + unmute: $ amixer sset Master unmute
    + Next, test to see if sound works:
        $ speaker-test -c 2

- Fonts:
    + `# pacman -S ttf-dejavu`

- Display:
    + To install the base Xorg packages:
        `# pacman -S xorg-server xorg-server-utils xorg-xinit`
    + Install mesa for 3D support:
        `# pacman -S mesa`
    + If you do not know which video chipset is available on your machine, run:
        `$ lspci | grep VGA`
    + For a complete list of open-source video drivers, search the package database:
        `$ pacman -Ss xf86-video | less`
    + The vesa driver is a generic mode-setting driver that will work with almost every GPU, but will not provide any 2D or 3D acceleration. If a better driver cannot be found or fails to load, Xorg will fall back to vesa. To install it:
        `# pacman -S xf86-video-vesa`
    + Laptop users (or users with a tactile screen) will need the xf86-input-synaptics package for the touchpad/touchscreen to work:
        `# pacman -S xf86-input-synaptics`
    + Test X (optional):
        = Install the default environment:
            # pacman -S xorg-twm xorg-xclock xterm
        = To start the (test) Xorg session, run:
            $ startx
        = A few movable windows should show up, and your mouse should work. Once you are satisfied that X installation was a success, you may exit out of X by issuing the exit command into the prompts until you return to the console.
            $ exit
        = If the screen goes black, you may still attempt to switch to a different virtual console (e.g. Ctrl+Alt+F2), and blindly log in as root. You can do this by typing "root" (press Enter after typing it) and entering the root password (again, press Enter after typing it).
        = You may also attempt to kill the X server with:
            # pkill X
        = If this does not work, reboot blindly with:
            # reboot

- Windows Management: dwm
    + Basic programming tools present in base-devel are needed in order to compile dwm and build a package for it, and the abs package is also a requisite for fetching the necessary build scripts. Installing dmenu, a fast and lightweight dynamic menu for X is a good idea.
        # pacman -S base-devel abs dmenu
    + Once the required packages are installed, use ABS to update and then copy the dwm build scripts from the ABS tree to a temporary directory. For example:
        # abs community/dwm
        $ cp -r /var/abs/community/dwm ~/dwm
    + Use cd to switch to the directory containing the build scripts (the example above used ~/dwm). Then run:
        $ makepkg -i
    This will compile dwm, build an Arch Linux package containing the resulting files, and install the package file all in one step. If problems are encountered, review the output for specific information.

    + To start dwm with startx or the SLIM login manager, simply append the following to ~/.xinitrc:
        exec dwm

### 1.4. System maintenance

- https://wiki.archlinux.org/index.php/System_maintenance

#### Check for errors

- Failed systemd services
    + `$ systemctl --failed`
    + https://wiki.archlinux.org/index.php/Systemd#Analyzing_the_system_state
- Log files
    + `# journalctl -p 3 -xb`
    + https://wiki.archlinux.org/index.php/Systemd#Journal
    + https://wiki.archlinux.org/index.php/Xorg#Troubleshooting

#### Backup

Backups may be automated with [systemd/Timers](https://wiki.archlinux.org/index.php/Systemd/Timers)

- Configuration files
- List of installed packages
- Pacman database
- LUKS headers
- System and user data

#### Upgrading the system


#### Use the package manager to install software


#### Clean the filesystem


## 2. Package management:

How to know your architecture: open terminal and type these command
- use command `# uname`
- use command **getconf**: `# getconf LONG_BIT`

+ find out with pkgfile: `$ pkgfile [filename]`
+ find binary's name: `$ pacman -Qlq package_name | grep /usr/bin/`
+ to see full list tools of pacman: `$ pacman -Ql pacman | grep bin`
+ update all package: `$ pacman -Syu`

Remember that pacman's output is logged in `/var/log/pacman.log`.

## 3. Booting

Something

## 4. Back up system

Back up your system before big upgrade. Use to recover your system when
it had trouble.

[Incremental back up][incremental-backup]: your data, important data.

[Non-incremental back up][non-incremental]
- [clonezilla](http://clonezilla.org/clonezilla-live-doc.php)

## 5. Graphical User Interface

### Display drivers

### Display server

### Window managers

### Display manager

## 6. Power management

Something

## 7. Multimedia

Something

## 8. Networking

Something

## 9. Input devices

Something

## 10. Optimization

Something

## 11. System service

Something

## 12. Appearance

Something

### Fonts

- ttf-inconsolata
- ttf-dejavu: DejavuSansMono
- Source Code Pro

## 13. Console improvements

Something

# Advanced

## Access control

### ACL

### LDAP

# Troubleshooting

## "Failed to commit transaction (conflicting files)" error

- A safe way is to first check if another package owns the file
    + pacman -Qo /path/to/file
- If the file is owned by another package, file a bug report.
- If the file is not owned by another package, rename the file which
  'exists in filesystem' and re-issue the update command. If all goes
  well, the file may then be removed.

## Merge two partitions

## Reinstall bootloader after install Windows

- Use live CD mount root partition under `/mnt` and run:
    + `syslinux-install_update -iamc /mnt`

# Contribution

## ArchWiki


## Software packaging

See more:
- arch-creating-pkg.md
- aur.md

# Tips & Tricks

## Live CD/USB/DVD images

- `archiso` package
    + https://wiki.archlinux.org/index.php/Archiso

## Install the linux-lts package

- Update your bootloader's configuration file to use the LTS kernel and
  ram disk: `vmlinuz-linux-lts` and `initramfs-linux-lts.img`

## Quit using python pip

- https://www.reddit.com/r/archlinux/comments/6vv5ty/guide_how_to_quit_using_pip_to_install_stuff/

## Resize the LVM logical volumes with LUKS (dm-crypt)

1. Boot to a live system using usb
2. Open the disk: `cryptsetup open /dev/sda2 encrypted-lvm`
3. Shrinking a logical volume and resize the file system at the same
   time: `lvresize -L -45GB -r /dev/vol-group1/logical-vol2`
4. Expanding a logical volume and resize the file system at the same
   time: `lvresize -l +100%FREE -r /dev/vol-group1/logical-vol2`
5. Diactivate the logical volumes: `vgchange -an`
6. Close the encrypted disk: `cryptsetup close encrypted-lvm`

## Remap Caps Lock key to Escape key + Automatically detect a plugging keyboard

This method can be using to remap any key automatically when the
keyboard is plugged in.

- Create a udev rule: `/etc/udev/rules.d/99-usb-keyboards.rules`

```bash
ACTION=="add", ATTRS{idVendor}=="04d9", ATTRS{idProduct}=="2013", RUN+="/home/glider/bin/kbd_udev", OWNER="glider"
```

- Install `at` package and start and enable `atd` service:

```bash
pacman -S at
systemctl start atd
systemctl enable atd
```

- Create two files: `/home/glider/bin/kbd` and
  `/home/glider/bin/kbd_udev` with permissions `755`

- `/home/glider/bin/kbd_udev` script:

```bash
#!/bin/bash
echo /home/glider/bin/kbd | at now
```

- `/home/glider/bin/kbd` script:

```bash
#!/bin/bash
sleep 0.1
DISPLAY=":0"
HOME=/home/glider/
XAUTHORITY=$HOME/.Xauthority
export DISPLAY XAUTHORITY HOME

setxkbmap -option caps:escape
```

Unset setxkbmap: `$ setxkbmap -option`

## Benchmarking

- [Benmarking](https://wiki.archlinux.org/index.php/Benchmarking)
- [Data storage devices](https://wiki.archlinux.org/index.php/Benchmarking/Data_storage_devices)

## Print

- CUPS

How to print
- Start cups service: `systemctl start org.cups.cupsd.service`
- Printer management: `http://localhost:631`

## Time

- Time for Linux, servers:
  [comparison](http://chrony.tuxfamily.org/comparison.html)

## [Default applications](https://wiki.archlinux.org/index.php/Default_applications)

# References

[awiki]: https://wiki.archlinux.org/
[forums]: https://bbs.archlinux.org/
[bugs]: https://bugs.archlinux.org/
[mailing-lists]: https://mailman.archlinux.org/mailman/listinfo/
[irc]: https://wiki.archlinux.org/index.php/IRC_channels
[international]: https://wiki.archlinux.org/index.php/International_communities
[involve]: https://wiki.archlinux.org/index.php/Getting_involved
[installation]: https://wiki.archlinux.org/index.php/Installation_guide
[base]: https://www.archlinux.org/groups/x86_64/base/
[download]: https://archlinux.org/download/
[dual-boot]: https://wiki.archlinux.org/index.php/Windows_and_Arch_Dual_Boot
[lvm]: https://wiki.archlinux.org/index.php/LVM
[encryption]: https://wiki.archlinux.org/index.php/Disk_encryption
[raid]: https://wiki.archlinux.org/index.php/RAID
[gparted]: http://gparted.sourceforge.net/livecd.php
[mirrors]: https://www.archlinux.org/mirrorlist/
[mirror-status]: https://www.archlinux.org/mirrors/status/
[post-installation]: https://wiki.archlinux.org/index.php/General_recommendations
[incremental-backup]: https://wiki.archlinux.org/index.php/backup_programs#Incremental_backups
[non-incremental]: https://wiki.archlinux.org/index.php/backup_programs#Non-incremental_backups
[netctl]: https://wiki.archlinux.org/index.php/Netctl
