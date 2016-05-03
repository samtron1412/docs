[TOC]

# Overview
Zathura is a free, plugin-based document viewer. It currently has plugins available for PDF, PostScript, and DjVu. It was written to be lightweight and controlled with vim-like keybindings.

# [Configuration](https://pwmt.org/projects/zathura/documentation/)
The customization of zathura is be managed via a configuration file called zathurarc. By default zathura will evaluate the following files:

	/etc/zathurarc
	$XDG_CONFIG_HOME/zathura/zathurarc (default: ~/.config/zathura/zathurarc)

# Keybindings
## Normal mode
	J, K   Go to the next or previous page

	h, k, j, l
	      Scroll to the left, down, up or right direction

	Left, Down, Up, Right
	      Scroll to the left, down, up or right direction

	^t, ^d, ^u, ^y
	      Scroll a half page left, down, up or right

	t, ^f, ^b, space, <S-space>, y
	      Scroll a full page left, down, up or right

	gg, G, nG
	      Goto to the first, the last or to the nth page

	^o, ^i Move backward and forward through the jump list

	^j, ^k Bisect forward and backward between the last two jump points

	^c, Escape
	      Abort

	a, s   Adjust window in best-fit or width mode

	/, ?   Search for text

	n, N   Search for the next or previous result

	o, O   Open document

	f      Follow links

	F      Display link target

	:      Enter command

	r      Rotate by 90 degrees

	^r     Recolor

	R      Reload document

	Tab    Show index and switch to Index mode

	d      Toggle dual page view

	F5     Switch to fullscreen mode

	^m     Toggle inputbar

	^n     Toggle statusbar

	=, -
	      Zoom in, out

	zI, zO, z0
	      Zoom in, out or to the original size

	n=     Zoom to size n

	mX     Set a quickmark to a letter or number X

	'X     Goto quickmark saved at letter or number X

	q      Quit

## Index mode
	k, j   Move to upper or lower entry

	l      Expand entry

	L      Expand all entries

	h      Collapse entry

	H      Collapse all entries

	space, Return
	      Select and open entry

# Commands
	bmark  Save a bookmark

	bdelete
	      Delete a bookmark

	blist  List bookmarks

	close  Close document

	exec   Execute an external command

	info   Show document information

	help   Show help page

	open, o
	      Open a document

	offset Set page offset

	print  Print document

	write, write!
	      Save document (and force overwriting)

	export Export attachments
