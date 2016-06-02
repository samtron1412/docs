[TOC]

# Overview
Vifm is an ncurses based file manager with vi like keybindings/modes/options/commands/configuration.

Help file: opening vifm and typing `:h`

- Trash directory: `~/.local/share/vifm/Trash`

# User Guide
## Basic hotkeys
	za          - Toggle the showing and hiding of dot files.
	t           - select or unselect (tag) the current file.
	Esc         - clear all selected files
	al          - puts symbolic links with absolute paths
	rl          - puts symbolic links with relative paths
	v           - enter visual mode
	ZQ          - quit program; same as :q!
	ZZ          - quit program; same as :wq

## Other hotkeys
### Panes
	Ctrl-W |  - maximize current view
	Ctrl-W =  - make size of two views equal
	Ctrl-W x  - exchange panes
	Ctrl-W s  - shortcut for :split (horizontal) or :sp
	Ctrl-W v  - shortcut for :vsplit (vertical) or :vs
	Ctrl-W o  - one full pane fullscreen ( same as :only or :o )

### Previewing
	e          - view selected files
	w          - preview files in the opposite pane
	:view      - display views of highlighted items like text files
	Shift-Tab  - enters view mode of selected item
		optional install:
		tree     - directory previews
		mp3info  - viewing information about mp3 files
		poppler  - pdf previews

### Bookmarks
	:marks               - list of bookmarks
	:marks list <term>   - search bookmarks
	dd                   - delete a boomark
	m[a-z][A-Z][0-9]     - to set a mark for the current file
	'[a-z][A-Z][0-9]     - moves to the file set for the mark

### Rename
	cw   - rename a file or files.
	cW   - change only name of file (without extension)
	A    - change only extension

# Customization
- [vifmrc template](https://github.com/vifm/vifm/blob/master/data/vifmrc)

## Color schemes

## Key mapping

## Opening filetypes in vifm

## User commands

## Marks

## Custom config (~/.vifm/vifmrc)
	" show all bookmarks
	nmap bm :marks <cr>

	" bookmarks
	mark h ~
	mark c ~/Documents
	mark d ~/Downloads
	mark e ~/Emulator
	mark p ~/Pictures
	mark g ~/Programs
	mark b ~/Public
	mark s ~/Storage
	mark t ~/Templates
	mark v ~/Videos
	mark m /media

	" copy files to the opposite pane
	nmap yy :!cp %f %D<cr>

	" move files to the opposite pane
	nmap dd :!mv %f %D<cr>

	" make a backup copy file in the same pane
	nmap yp :clone <cr>

	" trash-cli to handle trash
	nmap <delete> :!trash-put %f<cr>
	nmap u :!restore-trash <cr>
	nmap DD :!trash-empty <cr>

	" spacebar to select files; same as t (tag)
	nmap <space> t

	" quicker command line mode
	nmap ; :

	" quicker quitting program; it will resume where you left off
	nmap q ZZ

	" set color theme
	" https://github.com/jubalh/vifm-colors
	colorscheme solarized-dark

# Tips and Tricks
## start at different locations
	vifm .                       - start on current folder
	vifm ~/Download ~/Templates  - start on specific folder
