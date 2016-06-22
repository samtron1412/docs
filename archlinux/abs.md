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

## ABS overview
- **ABS tree**: The ABS directory structure containing files needed to build all official packages (but not the packages themselves nor the source files of the software).
	+ It is available in [svn](https://www.archlinux.org/svn/) and [git](https://projects.archlinux.org/svntogit/packages.git/) repositories and the `abs` script downloads them using rsync into `/var/abs/` on your machine.
	+ On the local system, the tree contains subdirectories for each repository specified in `/etc/abs.conf`.
	+ ABS tree sync once a day so it may lag behind what is already available in the repositories.
- **PKGBUILD**: A Bash script that contains the URL of the source code along with the compilation and packaging instructions.
- **makepkg**: shell command tool which reads the PKGBUILDs, automatically downloads and compiles the sources and creates a `.pkg.tar*` according to the `PKGEXT` array in `makepkg.conf`.
	+ You may also use makepkg to make your own custom packages from the AUR or third-party sources. See [Creating packages](https://wiki.archlinux.org/index.php/Creating_packages)
- **pacman**: a shell command tool, to install and remove the built packages and for fetching dependencies.
- **AUR**: The Arch User Repository is separate from ABS but AUR PKGBUILDs are built using makepkg to compile and package up software.
	+ The AUR exists as a website interface.
- **Warning**: Official PKGBUILDs assume that packages are [built in a clean chroot](https://wiki.archlinux.org/index.php/DeveloperWiki:Building_in_a_Clean_Chroot).
	+ Building software on a *dirty* build system may fail or cause unexpected behaviors at runtime, because if the build system detects dependencies dynamically, the result depends on what packages are available on the build system.

## Why would I want to use ABS?
- Compile or recompile a package, for any reason
- Make and install new packages from source of software for which no packages are yet available
- Customize existing packages to fit your needs (enabling or disabling options, patching)
- Compiling by using your compiler flags.
- Cleanly build and install your own custom kernel
- Get kernel modules working with your custom kernel
- Easily compile and install a newer, older, beta, or development version of an Arch package by editing the version number in the PKGBUILD.

# How to use ABS
Building packages using abs consists of these steps:
1. Install the `abs` package with `pacman`
2. Run `abs` as root to create the ABS tree by synchronizing it with the Arch Linux server.
3. Copy the build files (usually residing under `/var/abs/<repo>/<pkgname>`) to a build directory.
4. Navigate to that directory, edit the PKGBUILD (if desired/necessary) and do `makepkg`.
5. According to instructions in the PKGBUILD, `makepkg` will download the appropriate source, unpack it, patch (if desired), compile according to `CFLAGS` specified in `makepkg.conf`, and finally compress the built files into a package with the extension `.pkg.tar.gz` or `.pkg.tar.xz`.
6. Installing is as easy as doing `pacman -U <.pkg.tar.xz file>`. Package removal is also handled by `pacman`.

# Tips and Tricks
## Download sources
- Copy the package, whose source you want to have, from the local ABS tree (e.g. `/var/abs/core/findutils`) to another directory, e.g. `~/tmp/findutils`
- If you only want to get the sources and don't want to build the package then run: `makepkg -od`
- Build the package and handle all the package's dependencies automatically: `makepkg -s`
- Build your local sources (have your modifications): `makepkg -e`
