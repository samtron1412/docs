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

### Users and Groups management

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

### Privilege escalation

### Service management

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

### System maintenance

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

## 7. Multimedia

## 8. Networking

## 9. Input devices

## 10. Optimization

## 11. System service

## 12. Appearance

### Fonts

- ttf-inconsolata
- ttf-dejavu: DejavuSansMono
- Source Code Pro

## 13. Console improvements

# Advanced

## Access control

### ACL

### LDAP

# Troubleshooting

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
