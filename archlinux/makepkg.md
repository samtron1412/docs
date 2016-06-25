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
