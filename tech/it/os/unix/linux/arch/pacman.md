[TOC]

# Overview

- https://wiki.archlinux.org/title/Pacman
- The goal of pacman is to make it possible to easily manage packages,
  whether they are from the official repositories or the user's own
  builds.
- pacman keeps the system up-to-date by synchronizing package lists with
  the master server.
- pacman is written in C programming language.
- `pacman` will not remove configuration that the application itself
  creates (for examples "dotfiles" in the home folder).

# Concepts

## Packages

A package is an archive containing:
- all of the (compiled) files of an application
- metadata about the application, such as application name, version, dependencies, etc.
- installation files and directives for pacman

A virtual package is a special package which does not exist by itself, but is provided by one or more other packages.
- Virtual packages allow other packages to not name a specific package as a dependency, in case there are several candidates.
- Virtual packages cannot be installed by their name, instead they become installed in your system when you have installed a package providing the virtual package.
- An example is the dbus-units package.

### Cache

- https://wiki.archlinux.org/title/Pacman#Cleaning_the_package_cache
- Pacman stores its downloaded packages in /var/cache/pacman/pkg/ and
  does not remove the old or uninstalled versions automatically
- To move the cache directory to another location
    + https://wiki.archlinux.org/title/Pacman#Package_cache_directory

## Databases

pacman queries the local package database with the -Q flag, the sync
database with the -S flag and the files database with the -F flag.

The pacman databases are normally located at /var/lib/pacman/sync.
- For each repository specified in /etc/pacman.conf, there will be a corresponding database file located there.
- Database files are gzipped tar archives containing one directory for each package.


## Installation reason

The pacman database organizes installed packages into two groups,
according to installation reason:
- explicitly-installed: packages that were literally passed to a generic pacman -S or -U command;
- dependencies: packages that, despite never (in general) having been passed to a pacman installation command, were implicitly installed because they were required by packages explicitly installed.

Installation reason can be change and manually set.

## What happens during package install/upgrade/removal

When successful, the workflow of a transaction follows five high-level steps plus pre/post transaction hooks:

1. Initialize the transaction if there is not a database lock.
2. Choose which packages will be added or removed in the transaction.
3. Prepare the transaction, based on flags, by performing sanity checks on the sync databases, packages, and their dependencies.
4. Commit the transaction:
    1. When applicable, download packages (_alpm_sync_load).
    2. If pre-existing pacman PreTransaction hooks apply, they are executed.
    3. Packages are removed that are to-be-replaced, conflicting, or explicitly targeted to be removed.
    4. If there are packages to add, then each package is committed:
        1. If the package has an install script, its pre_install function is executed (or pre_upgrade or pre_remove in the case of an upgraded or removed package).
        2. pacman deletes all the files from a pre-existing version of the package (in the case of an upgraded or removed package). However, files that were marked as configuration files in the package are kept (see /Pacnew and Pacsave).
        3. pacman untars the package and dumps its files into the file system (in the case of an installed or upgraded package). Files that would overwrite kept, and manually modified, configuration files (see previous step), are stored with a new name (.pacnew).
        4. If the package has an install script, its post_install function is executed (or post_upgrade or post_remove in the case of an upgraded or removed package).
    5. If pacman PostTransaction hooks that exist at the end of the transaction apply, they are executed.
5. Release the transaction and transaction resource (i.e. database lock).

# Configuration

- `man pacman.conf`
- pacman settings are located in /etc/pacman.conf: this is the place
  where the user configures the program to work in the desired manner.

## General options

- General options are in the [options] section.

### Hooks

- pacman can run pre- and post-transaction hooks from the `/usr/share/libalpm/hooks/` directory;
- More directories can be specified with the `HookDir` option in `pacman.conf`, which defaults to `/etc/pacman.d/hooks`.
- Hook file names must be suffixed with `.hook`
- More information: `man alpm-hooks`

## Repositories and mirrors

Besides the special [options] section, each other [section] in
pacman.conf defines a package repository to be used.
- A repository is a logical collection of packages, which are physically
  stored on one or more servers: for this reason each server is called a
  mirror for the repository.

# User guide

- `man pacman`
- `pacman <operation> [options] [targets]`

## Operations

- `-D`, `--database`: modify the local package database
- `-Q`, `--query`: query the local package database
- `-R`, `--remove`
- `-S`, `--sync`: synchronize / install packages, search sync/remote database
- `-T`, `--deptest`: check dependencies, useful in scripts
- `-U`, `--upgrade`
- `-F`, `--files`: query the files database

## Installing packages

- To install packages: `# pacman -S pkg_name1 pkg_name2 ...`
- Install a 'local' package that is not from a remote repository (e.g
  the package is from the AUR):
    + `# pacman -U /path/to/package/package_name-version.pkg.tar.xz`
- Install a package from an unofficial remote location:
    + `# pacman -U http://www.example.com/repo/example.pkg.tar.xz`
- Download a package without installing it: `# pacman -Sw pkg_name`

## Removing packages

- To remove a package and leaving all of its dependencies still installed:
    + `# pacman -R pkg_name`
- To remove a package and its dependencies (recursively down):
    + `# pacman -Rs pkg_name`
- (DANGEROUS!!!) To remove a package, its dependencies and all the
  packages that depend on the target package: (recursively up and down!)
    + `# pacman -Rsc pkg_name`
- Remove all orphan packages: `# pacman -Rns $(pacman -Qtdq)`
- Remove everything but base group:
    + `# pacman -R $(comm -23 <(pacman -Qq|sort) <((for i in $(pacman -Qqg base); do pactree -ul $i; done)|sort -u|cut -d ' ' -f 1))`

## Upgrading packages

- To synchronize the repository database and update the system's
  packages (excluding "local" packages that are not in the configured
  repositories):
    + `# pacman -Syu`

## Query packages databases

- To query the local package database with the `-Q` flag: `$ pacman -Q --help`
- To query the sync / remote database with the `-S` flag: `$ pacman -S --help`
- To query the file database with the `-F` flag: `$ pacman -F --help`

### Sync/Remove Database

- To search for packages: `$ pacman -Ss string1 string2 ....`
- Search with regex to have more accurate results:
    + `$ pacman -Ss '^string$'`
- To display remote package information: `$ pacman -Si pkg_name`

### Local Package Database

- search for already installed packages:
    + `$ pacman -Qs string1 string2 ...`
- Display local package information: `$ pacman -Qi pkg_name`
- retrieve a list of the files installed by a package:
    + `$ pacman -Ql pkg_name` or `$ pacman -Qlq package | grep -v '/$' | xargs du -h | sort -h`
- list all dependency packages:
    + `$ pacman -Qd`
- list all packages no longer required as dependencies (orphans):
    + `$ pacman -Qdt`
- List all explicitly installed packages: `$ pacman -Qe`
- list all packages explicitly installed and not required as
  dependencies:
    +`$pacman -Qet`
- List all foreign packages (manually downloaded and installed): `$ pacman -Qm`
- List all native packages (installed from the sync database): `$ pacman -Qn`
- list all native (in sync databases) packages and explicitly installed:
    + `$ pacman -Qen`
- list all foreign packages and explicitly installed:
    + `pacman -Qem`
- list a dependency tree of a packages: `$ pactree pkg_name`
- list all the packages recursively depending on an installed package: `$ pactree -r pkg_name`
- List installed packages follow time install (use expac):
    + `expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -20`
- To list all installed packages sorted by size:
    +`$ expac -H M '%m\t%n' | sort -h` or `$ pacgraph -c`
	+ expac for more small packages
	+ with pacgraph you can draw image

### File Database

- Sync the files database before querying it to get up-to-date results:
    + `pacman -Fy`
- To search for package file names in remote packages:
    + `pacman -F string1 string2`
    + `pacman -F /path/to/file_name`: find which package contains this file
- To retrieve a list of the files installed by a remote package:
    + `pacman -Fl package_name`

## Cleaning package cache

Only do this when you are certain that previous package versions are not
required, for example for a later downgrade, if do this when you need
downgrade older versions would have to be retrieved through Archive
Arch.

- Remove cached versions of all packages (installed or uninstalled):
    + `paccache -r`: keep the most recent 3 versions
    + `paccache -rk5`: keep the most recent 5 versions
    + `paccache -rk1`: keep only the most recent version
- Remove cached versions of all uninstalled packages:
    + `paccache -ru`: keep the most recent 3 versions
    + `paccache -ruk5`: keep the most recent 5 versions
    + `paccache -ruk1`: keep only the most recent version
- (AVOID!) To remove all cache versions of removed packages: `# pacman -Sc`.
- (AVOID!) To remove all caches: `# pacman -Scc`

Enable and start paccache.timer to discard unused packages weekly.
- You can configure the arguments for the service in
  /etc/conf.d/pacman-contrib, e.g with PACCACHE_ARGS='-k1' or
  PACCACHE_ARGS='-uk0'

## Handling Config Files

- During an upgrade, 3 MD5 hashes of the original, current, and new
  files are calculated to make the decision.
- Based on the hashes, if pacman might create `.pacnew` file and warn
  users to merge these configurations manually.

# Tips and Tricks

- https://wiki.archlinux.org/title/Pacman/Tips_and_tricks

## Easy backup and restore

- https://wiki.archlinux.org/title/Pacman/Tips_and_tricks#List_of_installed_packages
- https://wiki.archlinux.org/title/Pacman/Tips_and_tricks#Back_up_the_pacman_database

### Backup and Reinstall pacman package lists

#### Option 1 - Found online

`pacman -Qqm` lists foreign packages name; which, for most users, means AUR
`pacman -Qqe` lists packages name that were explicitly installed.
that said,
  `pacman -Qqe | grep -v "$(pacman -Qqm)" > pacman.lst`
and
  `cat pacman.lst | xargs pacman -S --needed --noconfirm`
are the best backup/restore lines i've seen (don't remember where i got them tho).

#### Option 2: simpler version that I derived

- Native explicitly installed package list:
    + `pacman -Qqen > pacman-native.txt`
- Reinstall the native packages:
    + `cat pacman-native.txt | xargs pacman -S --needed --noconfirm`
- Foreign packages
    + `pacman -Qqm > pacman-foreign.txt`
    + This need to be reinstalled differently using AUR or manual
      approach.

# Troubleshooting

- https://wiki.archlinux.org/title/Pacman#Troubleshooting
- Remember that pacman's output is logged in `/var/log/pacman.log`

# References

1. [Arch Wiki - pacman][1]

[1]: https://wiki.archlinux.org/index.php/Pacman "Arch Wiki - pacman"
[tips]: https://wiki.archlinux.org/index.php/Pacman/Tips_and_tricks
