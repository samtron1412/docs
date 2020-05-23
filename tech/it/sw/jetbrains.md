# Overview

IDEs

# Tips and Tricks

## IdeaVim

- Reads the configuration from `~/.ideavimrc`
- Emulates some plugins
    + `set surround`: enable vim-surround

## External tools

- Open the current file at the current line in vim
    + `Preferences => Tools => External Tools`
    + Add a new external tool
    + Name: `vim`
    + Tool Settings
        * Program: `mvim`
        * Arguments: `+$LineNumber$ $FilePath$`
        * Working directory: `$FileDir$`
    + Create a key binding for this external tool
