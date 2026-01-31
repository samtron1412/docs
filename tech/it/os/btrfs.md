# Overview

- https://btrfs.readthedocs.io/en/latest/
- https://wiki.archlinux.org/title/Btrfs
- Btrfs is a modern Copy-on-Write (CoW) file system for Linux aimed at
  implementing advanced features while also focusing on fault tolerance,
  repair and easy administration.

# Configuring the file system

- Copy-on-Write (CoW) (implicit sharing or shadowing)
    + It is a resource-management technique used in programming to
      manage shared data efficiently.
        * Instead of copying data right away when multiple programs use
          it, the same data is shared between programs until one tried
          to modify it.
        * A copy is only made when needed, ensuring each program has its
          own version when modifications occur.
        * In traditional file systems, modifying a file overwrites the
          original data blocks in place. In CoW file system, the
          original blocks remain unchanged. When part of a file is
          modified, only the affected blocks are written to new
          locations, and metadata is updated to point to them,
          preserving the original version until it's no longer needed.
    + By default, btrfs uses CoW for all files all the time.
    + We can disable CoW if we want.
- Compression
    + `compsize` command can be used to view the status
        * `# compsize -x /`
- Subvolumes
    + https://btrfs.readthedocs.io/en/latest/Subvolumes.html#subvolume-flags
    + A btrfs subvolume is not a block device.
        * A subvolume can be viewed as a POSIX file namespace.
        * This namespace can be accessed via the top-level subvolume of
          the file system, or it can be mounted in its own right.
    + Each btrfs file system has a top-level subvolume with ID 5.
        * This subvolume cannot be removed or replaced.
        * Top-level subvolume has path `/` on the file system and other
          subvolumes are nested below the top-level subvolume.
        * However, subvolumes can be moved around in the file system and
          their path may change, whereas their ID cannot.
    + Listing subvolumes
        * `# btrfs subvolume list -t path`
    + Mount a subvolume:
        * using mount options `subvol=/path/to/subvolume` or
          `subvolid=objectid`
    + Create a subvolume:
        * Top-level subvolume must be mounted first.
        * `# btrfs subvolume create /path/to/subvolume`
    + Deleting a subvolume (or recursively all nested subvolumes)
        * MUST UNMOUNT SUBVOLUMES FIRST!!!
        * `# btrfs subvolume delete /path/to/subvolume`
        * `# btrfs subvolume delete --recursive /path/to/subvolume`

