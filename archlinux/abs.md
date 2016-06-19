[TOC]

# Overview
The **Arch Build System** is a **ports-like** system for building and packaging software from source code.
- While `pacman` is the specialized Arch tool for binary package management (including packages built with the ABS), ABS is a collection of tools for compiling source into installable `.pkg.tar.xz` packages.

## What is a ports-like system?
**Ports** is a system used by `*BSD` to automate the process of building software from source code.
- The system uses a **port** to `download, unpack, patch, compile, and install` the given  software.
- A **port** is merely a small directory on the user's computer, named after the corresponding software to be installed, that contains a few files with the instructions for building and installing the software from source.
	+ This makes installing software as simple as typing `make` or `make install clean` within the port's directory.

## ABS is a similar concept
ABS is made up of a directory tree (the ABS tree) residing under `/var/abs`.
- This tree contains many subdirectories, each within a repo name and each named by their respective package.
- This tree represents (but does not contain) all *official Arch software*, retrievable through the **SVN system**.
- You may refer to each package-named subdirectory as an `ABS`, much the way one would refer to a `port`.
- These ABS (or subdirectories) do not contain the software package nor the source but rather a `PKGBUILD` file (and sometimes other files).
	+ A `PKGBUILD` is a **simple Bash build script** - a text file containing the *compilation* and *packaging* instructions as well as the URL of the appropriate **source** tarball to be downloaded.
	+ By issuing inside the ABS `makepkg` command, the software is first compiled and then packaged within the build directory. Now you may use `pacman` to install, upgrade, and remove you new package.


# Tips and Tricks
## Download sources
- Copy the package, whose source you want to have, from the local ABS tree (e.g. `/var/abs/core/findutils`) to another directory, e.g. `~/tmp/findutils`
- If you only want to get the sources and don't want to build the package then run: `makepkg -od`
- Build the package and handle all the package's dependencies automatically: `makepkg -s`
- Build your local sources (have your modifications): `makepkg -e`
