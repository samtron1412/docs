[TOC]

# Overview
In Unix-like operating systems, any file or folder that starts with a dot character (for example, `/home/user/.config`), commonly called a dot file or `dotfile`, is to be treated as hidden – that is, the `ls` command does not display them unless the `-a` flag (`ls -a`) is used.

The notion that filenames preceded by a `.` should be hidden in Unix was probably an unintended consequence of trying to make `ls` not show `.` and` ..`. [A lesson from shortcuts](https://plus.google.com/u/0/+RobPikeTheHuman/posts/R58WgWwN9jp)

A convention arose of using dotfile in the user's home directory to store per-user configuration or informational text. Dotfiles are used to customize your system with purpose is improving your productivity.

# Why use dotfiles with VCS (version control system)?
- Distributed backups: exploring new things without fear + restoring when disaster happen.
- History: improving yourself, debug
- Sharing: learn from each other + making life more meaningful

# How can we manage the dotfiles?
- Most likely, as a developer, you will keep using and improving your dotfiles for your entire career. Your dotfiles will most likely be the *longest project you ever work on*. For this reason, it is worthwhile to organize your dotfiles project in a disciplined manner for **maintainability** and **extensibility**.

## Organizational Approaches
- Having your entire home directory under VCS (and ignore/exclude files which you don't want to commit)
- Keeping your configuaration files in a seperate directory and symlink them into place. This approache is vastly superior for sevveral reasons:
	+ There is no possibility of accidentally deleting your files. With your entire home directory under VCS, running something like a `git clean` could wipe out everything in your home directory that is not tracked by your VCS.
	+ It is possible to track configuration files that belong somewhere other than `$HOME`.
	+ Installing dotfiles on new machines is easier. All that is required is cloning your dotfiles followed by linking files. Keepping the entire home directory under VCS complicates installation.

## Process
1. Create a new folder to store your dotfiles (e.g. `~/dotfiles`).
2. Copy everything to it. You should copy to another places to back it up.
3. Create symlinks to new place files replaced for dotfiles in `$HOME`.
4. Put `~/dotfiles` to VCS.
5. Write install/bootstrap file to install dotfiles on new systems.

## Installation

## Dependencies and Plugins
- Using `git submodules`

Adding new submodule to your repository:

	git submodule add <git-repo-link> [<path>]
	git submodule add https://github.com/robbyrussell/oh-my-zsh ~/.dotfiles/.oh-my-zsh
	git submodule add https://github.com/robbyrussell/oh-my-zsh

Initializing all your submodules and checking out the specified versions:

	git submodule update --init --recursive

Upgrading submodules from the upstream changes:

	git submodule update --init --remote

## Local Customization
When managing dotfiles on multiple machines, the majority of your configuration will be the same between machines, and there will be some minor differences between installations.

### Approaches
- Using branches in your main dotfiles repository.
- Having a main do[tfiles repository and a separate repository for local customizations that override defaults (e.g. [dotfiles-local](https://github.com/anishathalye/dotfiles-local) repository).
	+ This has the additional advantage that your main dotfiles can be open sourced, and your local customizations can be kept private.
	+ It's cleanest way.
	+ This secondary repository should have branches for all your different machines (or groups of machines). You should have an install script for this repository as well.

### Applying local customizations
**Shell**: you can add the following to the end of your *shell rc* file to enable overriding

	if [ -f ~/.zshrc-local ]; then
		source ~/.zshrc-local
	fi

**Git**: you can add the following to the end of your `.gitconfig` file to enable overriding

	[include]
		path = ~/.gitconfigl-local

**Vim**: you can add following to the end of your `.vimrc` file to enable overriding

	let $LOCALFILE=expand("~/.vimrc-local")
	if filereadable($LOCALFILE)
		source $LOCALFILE
	endif

## Miscellaneous Tips
### Path to dotfiles directory
Having a persistent path to your dotfiles repository. This can be done by always keeping your dotfiles in a specific directory such as `~/.dotfiles`. You can create a symbolic link from `~/.dotfiles` to your dotfiles as a part of your installation process.

### Tracking Custom Scripts
Creating a `bin/` directory in dotfiles directory for your shell scripts, link `~/bin` with that directory in installation process, and then add the following to your shell rc file `export PATH=~/bin:${PATH}`
