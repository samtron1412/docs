[TOC]

# Overview

Cheatsheet
- https://quickref.me/homebrew

# Usage

```
# Homebrew gathers anonymous aggregated user behavior analytics and reports these to Google Analytics. It is recommended that you choose to opt out
# See https://github.com/Homebrew/brew/blob/master/docs/Analytics.md for the detail.
brew analytics off
```

- Description of a package: `brew desc <pkg>`
- Install: `brew install <pkg>`
- Uninstall: `brew uninstall <pkg>`
- Update: `brew update`
- List outdated packages: `brew outdated` and `brew outdated --cask`
- Upgrade: `brew upgrade`
- List all packages: `brew list`
- Search a package: `brew search <text>`
- Cleaning up
    + Showing old version of packages: `brew cleanup -n`
    + Cleaning up all old versions: `brew cleanup`
    + Cleaning up old versions of a package: `brew cleanup <pkg>`
    + Removing the whole caches: `rm -rf "$(brew --cache)"`
- Dependencies
    + Showing dependencies of a package: `brew deps <pkg>`
    + Showing dependencies as tree for a package: `brew deps --tree pkg`
    + Showing dependencies as tree for all installed packages:
        * `brew deps --tree --installed`
    + Showing list of dependencies for all installed packages:
        * `brew deps --installed`
- Showing packages that are not dependencies of another installed
  packaged: `brew leaves`
- Info
    + Summary info for packages/formulae: `brew info`
    + Summary info for taps: `brew tap-info`
- Tap
    + List all installed taps: `brew tap`
    + Tap a package repository: `brew tap <user/repo>`
    + Remove a tap: `brew untap <tapname:user/repo>`
- Different versions of a package
    + `brew tap homebrew/cask-versions`
- Stop upgrading a certain package
    + `brew pin package`
    + `brew unpin package`
    + `brew list --pinned`
- Install older versions of brew package
    + Similar casks, only change the command
    + `brew install ...` instead of `brew cask install ...`

# Cask

## Usage ##

- Cask: install macOS applications distributed as binaries
    + commands: info, install, uninstall, list, outdated, upgrade
    + after the name of a cask, if it has "auto_updates": it means that
      the package has a mechanism to update itself, so brew cask does
      not upgrade the package
- Install Older Versions of Brew Casks
    + Go to the Homebrew Cask's GitHub page: https://github.com/caskroom/homebrew-cask
    + Click `Find file` to find `<package>.rb`: e.g., `mendeley.rb`
    + Find the raw file of the older version
    + `brew cask install https://raw.githubusercontent.com/ran-dall/homebrew-cask/151f569163295a1b924fb737eb9788dcb9ac263f/Casks/mendeley.rb`

## Writing a formula ##

- Cask language references: https://github.com/Homebrew/homebrew-cask/tree/master/doc
    + Stanzas (variables in a formula): https://github.com/Homebrew/homebrew-cask/tree/master/doc/cask_language_reference/stanzas

# Bundle

+ Install
    * `brew bundle`: looking for `Brewfile` in the current directory
      and install all the formulae in the file
    * `brew bundle --file <path/to/a/different/Brewfile>`
+ Dump
    * `brew bundle dump`: create a `Brewfile` from all existing
      Homebrew packages at the current directory
    * `brew bundle dump --force`: overwrite an existing Brewfile
    * `brew bundle dump [--force] --describe`: output a description
      comment above each line
+ Cleanup
    * `brew bundle cleanup`: listing all packages that are not
      listed in the Brewfile
    * `brew bundle cleanup --force`: uninstall them
+ Check: `brew bundle check [--verbose]`
+ List
    * `brew bundle list --all [--casks, --taps, --mas, --brews]`
    * default `--brews`


# mas: Mac App Store

- `mas list`
- `mas search Xcode [--price]`
- `mas install <app_id>`: application identifier
- `mas outdated`
- `mas upgrade` or `mas upgrade <app_id>`
- `mas signin --dialog mas@example.com`: sign in
- `mas account`: account info
- `mas info <app_id>`
- `mas uninstall <app_id> [--dry-run]`
- `mas version`


# Tips and Tricks #

- Remove a package with its dependencies:
    + `brew tap beeftornado/rmtree`
    + `brew rmtree <pkg>`
