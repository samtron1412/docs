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

## Details
1. `$ sudo pacman -S abs`
2. Modify `/etc/abs.conf` to include your desired repositories. Remove the `!` in front of the appropriate repositories.
	- `REPOS=(core extra community !testing)`
	- Download ABS tree: `$ sudo abs`
	- Individual ABS package files: `$ sudo abs <repository>/<package>`
	- `~/.makepkg.conf` set `PACKAGER="myname <myemail@myserver.com>"`. It allows a "flag" to quickly identify which packages have been built and/or installed by you, not the official maintainer.
		+ Showing all packages:  `$ expac "%n %p" | grep "myname" | column -t`
		+ Showing only packages contained in repos: `$ . /etc/makepkg.conf; grep -xvFf <(pacman -Qqm) <(expac "%n\t%p" | grep "$PACKAGER$" | cut -f1)`
3. Create a build directory: `$ mkdir -p ~/abs`. Copy the ABS from the tree to the build directory.
4. Build package: `$ makepkg -s`
5. **fakeroot**
	- Essentially, the same steps are being executed in the traditional method (`.configure, make, make install` steps).
	- But the software is installed into a `fake root` environment.
	- A fake root is simply a subdirectory within the build directory that functions and behaves as the system's root directory. `makepkg` creates a fake root directory, and installs the compiled binaries and associated files into it, with root as owner.
	- The fake root, or subdirectory tree containing the compiled software, is then compressed into and archive `.pkg.tar.xz`.
	- When invoked, pacman then extracts the package (installs it) into the system's real root directory `/`.


# Patching in ABS
## Creating patches
If you need to edit source code, make files, configuration files, etc, you will need to be able to create a patch.

>If you need only to change one or two lines in a file (e.g. a Makefile), you may be better off investigating the properties of `sed` instead.

Creating a patch for a package involves creating two copies of the package, editing the new copy, and creating a unified diff between the two files. When creating an Arch Linux package, this can be done as follows:
1. Add the download source of the file to the source array of the `PKGBUILD` you are creating. If you are altering an existing PKGBUILD, this step is taken care of.
2. Create a dummy (empty, or containing a single `echo` command) `build()` function. If you are altering an existing `PKGBUILD`, you should comment out most of the lines of the build function, as you are going to be running `makepkg` several times, and you will not want to spend a lot of time waiting for a broken package to build.
3. Run `makepkg -o`: this will download the source files you need to edit into the `src` directory.
4. Change to the `src` directory. In standard cases, there will be a directory containing a bunch of files that were unzipped or untarred from a downloaded archive there. You should make two copies of these directories. One is a pristine copy that makepkg will not be allowed to manipulate, and one will be the new copy that you will create a patch from. You can name the two copies `pkg.pristine` and `pkg.new` or something similar.
5. Change into the `pkg.new` directory. Edit whichever files need to be edited. The changes needed depend on what the patch has to do; it might correct a Makefile paths, it may have to correct source errors, and so on. You can also edit files in subfolders of the `pkg.new` directory. Do not issue any commands that will inadvertently create a bunch of files in the `pkg.new` directory; i.e. do not try to compile the program to make sure your changes work. The problem is that all the new files will show up in the patch, and you do not want that. Instead, apply the patch to another copy of the directory (not the pristine directory), either manually with the `patch` command, or in the `PKGBUILD` and test the changes from there.
6. Change back to the `src` directory.
7. Run `diff -aur pkg.pristine pkg.new`. This will output all the changes you made in unified diff format. You can scan these to make sure the patch is good.
8. Run `diff -aur pkg.pristine pkg.new > pkg.patch` to capture all the changes in a file named `pkg.patch`. This is the file that will be used by patch. You may now apply the changes to a copy of the original directory and make sure they are working properly. you should also check to ensure that the patch does not contain any extraneous details. For example, you do not want the patch to convert all tabs in the files you edited to spaces because your text editor did that behind your back. You can edit the patch either using a text editor, or to be safer, edit the original files and create the patch afresh.



# Tips and Tricks
## Download sources
- Copy the package, whose source you want to have, from the local ABS tree (e.g. `/var/abs/core/findutils`) to another directory, e.g. `~/tmp/findutils`
- If you only want to get the sources and don't want to build the package then run: `makepkg -od`
- Build the package and handle all the package's dependencies automatically: `makepkg -s`
- Build your local sources (have your modifications): `makepkg -e`

## Preserve modified packages
Insert a group array into the PKGBUILD, and add the package to a group called `modified`.

	PKGBUILD
	groups=('modified')

Add this group to the section `IgnoreGroup` in `/etc/pacman.conf`.

If new versions are available in the official repositories during a system update, pacman prints a note that it is skipping this update because it is in the IgnoreGroup section. **At this point the modified package should be rebuilt from ABS to avoid partial upgrades.**

