[TOC]

# [Overview](https://en.wikipedia.org/wiki/Vim_(text_editor))
## History
Initial release in November 1991.

## Help
`:help` help facility built-in
`vimtutor` : basic commands tutorials
`:h key-notation`: these names for keys are used in the documentation.

## Features and improvements over vi
### Customization
Part of Vim's power is that it can be extensively customized.
- Change basic interface
- Define personalized key mappings
- Abbreviations to automate sequences of keystrokes
- Call internal or user defined functions

Plugins available that will extend or add new functionality to Vim.
- Vim's internal scripting language - vimscript (viml)
- Lua, Perl, Python, Raccket, Ruby, and Tcl

### Search and replace
- Change each "foo" to "bar" in the current line: `:s/foo/bar/g` and have confirm : `:s/foo/bar/gc`
- Change each "foo" to "bar" in all the lines: `:%s/foo/bar/g` and have confirm: `:%s/foo/bar/gc`
- Change each "foo" to "bar" for all lines from line 5 to line 12: `:5,12s/foo/bar/gc`

### Copy and paste
- Config at `.vimrc` : `xnoremap p pgvy` it mean *p* will replay with *pgvy*, *p* to paste and *gv* to re-select what was originally selected, *y* to copy it again.
- Paste multiple copy: *<number>p* e.g: *30p* to paste 30 time of copy text.

### Others
- Completion
- Comparison and merging of files - vimdiff
- Extended regular expressions
- Graphic user interface - gvim
- Spell checking
- Folding
- Tabbed windows
- Unicode and other multilanguage support
- Syntax highlight
- etc.

## Resources
- [Documentation](http://vimdoc.sourceforge.net/htmldoc/usr_toc.html)
- [summary](http://vimdoc.sourceforge.net/)
http://vim.wikia.com/wiki/Vim_Tips_Wiki
http://vim.wikia.com/wiki/Vim_documentation
http://vim.wikia.com/wiki/Vim_scripts
http://www.vim.org/docs.php
- [Books](http://iccf-holland.org/click5.html)
- [Thoughtbot Tutorials](https://upcase.com/vim)

# Getting started
## The Dot command
The dot command lets us repeat the last change.
- The last change could be one of many things. A change could act at the level of individual characters, entire lines, or even the whole file.
- From the moment we enter Insert mode until we return to Normal mode, Vim records every keystroke. After making a change such as this, the dot command will replay all keystrokes.
- The dot command is a micro macro

## Undo - Redo in normal mode
`u`: undo
`Ctrl + r`: redo

# The VIM way
Vim is optimized for repetition. Its efficiency stems from the way it tracks our most recent actions.We can always replay the last change with a single keystroke. We need to learn to craft our actions so that they perform a useful  unit of work when replayed. Mastering this concept is the key to becoming effective with Vim.

# Tips and Tricks
## [Accessing the system clipboard](http://vim.wikia.com/wiki/Accessing_the_system_clipboard)

## [Fix meta key in terminal](http://stackoverflow.com/questions/6778961/alt-key-shortcuts-not-working-on-gnome-terminal-with-vim)

## [Moving lines up and down](http://vim.wikia.com/wiki/Moving_lines_up_or_down)

## [Work with multiple files](http://stackoverflow.com/questions/53664/how-to-effectively-work-with-multiple-files-in-vim)

## Show hidden characters like carriage return and linefeed

`vim -b <file>`: show carriage return

`:set list`: to show linefeed

# Tuning Vim
## Vim script
Vim script (`viml`) is the scripting language built into Vim. Based on the ex editor language of the original vi editor.

Vim script files are stored in plain text format and the file name extension is `.vim`.

## Plug-in manager
- Discusses:
	+ http://vi.stackexchange.com/questions/388/what-is-the-difference-between-the-vim-package-managers
	+ https://www.reddit.com/r/vim/comments/36ak7j/do_you_use_a_vim_plugin_manager_if_so_which_one/
	+ https://www.reddit.com/r/vim/comments/1w4udb/best_vim_plugin_manager/
- [Vim-plug](https://github.com/junegunn/vim-plug)
- [pathogen](https://github.com/tpope/vim-pathogen/)
- [Vundle](https://github.com/VundleVim/Vundle.vim)
- [NeoVundle](https://github.com/Shougo/neobundle.vim)

## [.vimrc template](http://www.vimbits.com/)
- http://alvinalexander.com/linux-unix/vimrc-vim-example-commands-configuration-file
- [change color of vim](http://alvinalexander.com/linux/vi-vim-editor-color-scheme-colorscheme)
`:colorscheme delek` or `:colo delek`
`:syntax on`
- Copy text and paste and recopy it to paste more time: `xnoremap p pgvy`
- [.vimrc template](http://amix.dk/vim/vimrc.html)
- [A good vimrc](http://dougblack.io/words/a-good-vimrc.html)
- [.vimrc template 2](http://spf13.com/post/perfect-vimrc-vim-config-file)
- [ultimate configuration](https://github.com/amix/vimrc)

Example:

```vim
set number
colo delek
syntax on
set backup
set backupdir=/tmp/vim
set dir=/tmp/vim/swap
set hlsearch
set incsearch
set ignorecase
set expandtab
set smarttab
set shiftwidth=2
set tabstop=2
set autoindent
set smartindent
set wrap
```

## Plugins
### [Powerline](https://github.com/powerline/powerline)

# [NeoVim](https://github.com/neovim/neovim) - A new generation of Vim
Neovim is a refactor of Vim, that strives to be a superset of Vim.
- Neovim shares the same configuration syntax with Vim.
- Neovim can execute plugins asynchronously.
- Neovim's plugins can also be written in any language.

# Troubleshooting


# References
