[TOC]

# Overview

Logical Volume Management (LVM) is a disk management option that every
major Linux distribution includes.

# What is LVM?

LVM allows for a layer of abstraction between your operating system and
the disks/partitions it uses.

In traditional disk management your operating system looks for what
disks are available (/dev/sda, /dev/sdb, etc.) and then looks at what
partitions are available on those disks (/dev/sda1, /dev/sda2, etc.).

With LVM, disks and partitions can be abstracted to contain multiple
disks and partitions into one device. Your operating systems will never
know the difference because LVM will only show the OS the **volume
groups (disks)** and **logical volumes (partitions)** that you have set
up.

# Common uses

Because volume groups and logical volumes aren't physically tied to a
hard drive, it makes it easy to dynamically resize and create new disks
and partitions. In addition, LVM can give you features that your file
system is not capable of doing. For example, Ext3 does not have support
for live snapshots, but if you're using LVM you have the ability to take
a snapshot of your logical volumes without unmounting the disk.

- Managing large hard disk farms by allowing disks to be added and
  replaced without downtime or service disruption, in combination with
  hot swapping (term used to describe the functions of replacing
  computer system components without shutting down the system).
- Allows file systems to be easily resized later as needed.
- Performing consistent backups by taking snapshots of the logical
  volumes.
- Creating single logical volumes of multiple physical volumes or entire
  hard disks (like to RAID 0), allowing for dynamic volume resizing.

# Anatomy of LVM

```
    hda1   hdc1      (PV:s on partitions or whole disks)
       \   /
        \ /
       diskvg        (VG)
       /  |  \
      /   |   \
  usrlv rootlv varlv (LV:s)
    |      |     |
 ext2  reiserfs  xfs (filesystems)
```

LVM internal organization

![lvm internal](linux/lvm_internal.gif)

- **Volume group (VG)**: is the highest level abstraction used within
  the LVM. It gathers together a collection of Logical Volumes and
  Physical Volumes into one administrative unit.
- **Physical Volume (PV):** is typically a hard disk, though it may well
  just be a device that 'looks' like a hard disk (eg. a software raid
  device)
- **Logical Volume (LV):** equivalent of a disk partition in a non-LVM
  system. The LV is visible as a standard block device; as such the LV
  can contain a file system (eg. /home).
- **Physical Extent (PE):** each physical volume is divided chunks of
  data, known as physical extents, these extents have the same size as
  the logical extents for the volume group.
- **Logical Extent (LE):** each logical volume is split into chunks of
  data, known as logical extents. The extent size is the same for all
  logical volumes in the volume group.

Mapping logical extents to physical extents. Each PV consists of a
number of fixed-size physical extents (PEs); similarly, each LV consists
of a number of fixed-size logical extents (LEs). (LEs and PEs are always
the same size, the default in LVM 2 is 4 MB.)

![lvm mapping](linux/lvm_mapping.gif)

Linear mapping

![lvm linear mapping](linux/linear_mapping.gif)

Striped mapping

![lvm striped mapping](linux/striped_mapping.gif)


# LVM command line tool

- Physical Volume = pv
  + The physical volume commands are for adding or removing hard drives
    in volume groups.
- Volume Group = vg
  + The volume group commands are for changing what abstracted set of
    physical partitions are presented to your operating system in
    logical volumes.
- Logical Volume = lv
  + Logical volume commands will present the volume groups as partitions
    so that your operating system can use the designated space.

![lvm-cheatsheet](linux/lvm-cheatsheet.png)

## View current LVM information

`pvdisplay`, `vgdisplay`, `lvdisplay`

# References

[pros-cons]: http://www.gossamer-threads.com/lists/gentoo/user/156658 "Gentoo Mailing list - LVM pros and cons"
