# Overview

A Linux distribution based on Debian.
- 3 editions: Desktop, Server, and Core (IoT)
- Ubuntu is released every 6 months, with long-term support (LTS)
  releases every two years.

# Package Manager

## Introduction

Ubuntu's package management system is derived from the same system used
by the Debian GNU/Linux distribution.
- The package files contain all of the necessary files, meta-data, and
  instructions to implement a particular functionality or software
  application.
- `.deb`: package file
    + dependencies: additional packages required by the principal
      package

## Configuration: System Repositories

- `/etc/apt/sources.list` file
- `/etc/apt/sources.list.d` directory

## Apt

Ubuntu's Advanced Packaging Tools (APT)
- `apt` tool is intended to be used interactively, and not to be called
  from non-interactive scripts.
- `apt-get` command should be used in scripts, perhaps with the
  `--quiet` flag.
- Actions of `apt` command are logged in the `/var/log/dpkg.log` file.
- `apt help`: further information about the use of APT

- Install a package: `sudo apt install pkg`
- Remove a package: `sudo apt remove pkg`
    + Adding `--purge` option will remove the package configuration
      files as well.
- Update the package index: `sudo apt update`
    + a database of available packages from the repositories defined in
      the `/etc/apt/sources.list` file and in the
      `/etc/apt/sources.list.d` directory.
- Upgrade Packages: `sudo apt upgrade`
- Actions are logged in `/var/log/dpkg.log`
- Help: `apt help`

## Aptitude

- Launching Aptitude with no command-line options => a menu-driven,
  text-based front-end to `apt`.
    + `sudo aptitude`
- You can use `aptitude` as command-line tool similar to apt.
    + `sudo aptitude install nmap`

## dpkg (Debian Packager)

>**NOTE**: `dpkg` does not handle dependencies

- `dpkg` is a package manager for Debian-based systems.
- List all packages: `dpkg -l`
- List files installed by a package: `dpkg -L nmap`
- Determine which package installed a file: `dpkg -S /etc/host.conf`
    + The output will show the package that installed the file.
- Install a local `.deb` file: `sudo dpkg -i zip_amd64.deb`
- Uninstalling a package: `sudo dpkg -r zip`
    + Does not handle DEPENDENCIES !!!

# Upgrading

## do-release-upgrade

- This utility is installed by default.
- Typing in a terminal: `do-release-upgrade`
- On an LTS system, to update to a new system before the first point
  release, e.g., if you want to upgrade from 18.04 to 20.04 before
  20.04.1 is released.
    + Using `-d` switch: `sudo do-release-upgrade -d`
- bluetoothctl
    + The devices need to have a status of `Not Set Up`: holding down
      power button of devices
