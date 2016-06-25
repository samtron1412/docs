[TOC]

# Overview
**makepkg** is a script to automate the building of packages.

The requirements for using the script are:
- a build-capable Unix platform
- a PKGBUILD.

makepkg is provided by the `pacman` package.

# Configuration
See `man makepkg.conf` for details.

The system configuration: `/etc/makepkg.conf`

User-specific changes: `$XDG_CONFIG_HOME/pacman/makepkg.conf` or `~/.makepkg.conf`

## Packager information
Each package is tagged with metadata identifying among others also the **packager**. Set `PACKAGER` variable in `makepkg.conf`

	PACKAGER="John Doe <john@doe.com"

To automatically produce signed packages, also set the `GPGKEY` variable in `makepkg.conf`.

## Package output
- `BUILDDIR=/tmp/makepkg`: build directory
- `PKGDEST=~/pkg`: resulting packages
- `SRCDEST=~/src`: downloaded sources
- `SRCPKGDEST=~/srcpkg`: resulting source packages (built with `makepkg -S`)

## Signature checking
If a signature file in the form of `.sig` or `.asc` is part of the PKGBUILD source array, makepkg automatically attempts to verify it.

In case the user's keyring does not contain the needed public key for signature verification, makepkg will abort the installation with a message that the PGP key could not be verified.

If a needed public key is missing, or if you want to add public keys by other developers, you can:
- [import it manually](https://wiki.archlinux.org/index.php/GnuPG#Import_a_key)
- or find it [on a keyserver](https://wiki.archlinux.org/index.php/GnuPG#Use_a_keyserver) and import it from there
- temporarily disable makepkg's signature checking, by calling `makepkg` with the `--skippgpcheck` option.

The signature checking implemented in makepkg does not use pacman's keyring, instead relying on the user's keyring.[1](http://allanmcrae.com/2015/01/two-pgp-keyrings-for-package-management-in-arch-linux/)

# Usage
- Install the `base` and `base-devel` groups.
- Running makepkg itself as root is disallowed. [2](https://projects.archlinux.org/pacman.git/tree/NEWS)
- Besides how a `PKGBUILD` may contain arbitrary commands, building as root is generally considered unsafe. [3](https://bbs.archlinux.org/viewtopic.php?id=67561)

Build a package:
- Create a `PKGBUILD`, or build script
- Change to the directory and issue commands
	+ Automatically install needed dependencies: `$ makepkg -s`
	+ Adding the `-r`/`--rmdeps` flags causes makepkg to remove the make dependencies later, which are no longer needed. Or use pacman trick removing unused packages (orphans) once in a while instead.
	+ To install a package use `-i`/`--install` (same as `pacman -U pkgname-pkgver.pkg.tar.xz`): `$ makepkg -i`
	+ To clean up leftover files and folders, such as files extracted to the `$srcdir`, add the flag `-c`/`--clean`. This useful for multiple builds of the same package or updating the package version, while using the same build folder. It prevents obsolete and remnant files from carrying over to the new builds: `$ makepkg -c`

# Tips and tricks
## Creating optimized packages
- Using automatically detect and enable safe architecture-specific optimizations (as of version 4.3.0 of GCC)
	+ Fist remove any `-march` and `-mtune` flags
	+ Add `-march=native`
	+ `CFLAGS="-march=native -O2 -pipe -fstack-protector-strong"`
	+ `CXXFLAGS="${CFLAGS}"`
	+ To see what flags this enables on your machine: `$ gcc -march=native -v -Q --help=target`

## MAKEFLAGS
The `MAKEFLAGS` option can be used to specify additional options for make.

Users with multi-core/multi-processor systems can specify the number of jobs to run simultaneously. `MAKEFLAGS="-j$(nproc)"`

Some `PKGBUILDs` specifically override this with `-j1`, because of race conditions in certain versions or simply because it is not supported in the first place.

Packages that fail to build because of this should be reported on the bug tracker (or in the case of AUR packages, to the package maintainer)

## Improving compile times
### tmpfs
As compiling requires many I/O operations and handling of small files, moving the working directory to a tmpfs may bring improvements in build times. `BUILDDIR=/tmp/makepkg`

>Avoid compiling larger packages in tmpfs to prevent running out of memory.

Any package compiled in tmpfs will not persist across reboot. Consider setting the PKGDEST option appropriately to move the built package automatically to another (persistent) directory.

### ccache
Using ccache

## Generate new checksums
`$ updpkgsums`

## Create uncompressed packages
Set `PKGEXT='.pkg.tar'` in `/etc/makepkg.conf`

## Utilizing multiple cores on compression
`xz` supports symmetric multiprocessing via the `--threads` flag to speed up compression. `COMPRESSXZ=(xz -c -z - --threads=0)`

