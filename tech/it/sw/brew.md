[TOC]

# Overview

# Usage

- Description of a package: `brew desc <pkg>`
- Install: `brew install <pkg>`
- Uninstall: `brew uninstall <pkg>`
- Update: `brew update`
- Upgrade: `brew upgrade`
- List all packages: `brew list`
- Search a package: `brew search <text>`
- Cleaning up
    + Showing old version of packages: `brew cleanup -n`
    + Cleaning up all old versions: `brew cleanup`
    + Cleaning up old versions of a package: `brew cleanup <pkg>`
- Dependencies
    + Showing dependencies of a package: `brew deps <pkg>`
    + Showing dependencies as tree for a package: `brew deps --tree pkg`
    + Showing dependencies as tree for all installed packages:
        * `brew deps --tree --installed`
    + Showing list of dependencies for all installed packages:
        * `brew deps --installed`
- Showing packages that are not dependencies of another installed
  packaged: `brew leaves`
- Tap
    + List all installed taps: `brew tap`
    + Tap a package repository: `brew tap <user/repo>`
- Info
    + Summary info for packages/formulae: `brew info`
    + Summary info for taps: `brew tap-info`
- Cask: install macOS applications distributed as binaries
    + commands: info, install, uninstall, list, outdated, upgrade
    + after the name of a cask, if it has "auto_updates": it means that
      the package has a mechanism to update itself, so brew cask does
      not upgrade the package
- Remove a package with its dependencies:
    + `brew tap beeftornado/rmtree`
    + `brew rmtree <pkg>`
