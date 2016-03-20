[TOC]

# Overview
Zathura is a free, plugin-based document viewer. It currently has plugins available for PDF, PostScript, and DjVu. It was written to be lightweight and controlled with vim-like keybindings.

# [Configuration](https://pwmt.org/projects/zathura/documentation/)
The customization of zathura is be managed via a configuration file called zathurarc. By default zathura will evaluate the following files:

	/etc/zathurarc
	$XDG_CONFIG_HOME/zathura/zathurarc (default: ~/.config/zathura/zathurarc)

# Default keybindings
	h: scroll to the left
	l: scroll to the right
	j: scroll downward
	k: scroll upward
	o: open a file
	a: zoom to fit the page
	s: zoom to fit the width of the page
	F5: toggle full screen mode
	+: zoom in
	-: zoom out
	=: to the original size
	q : quit Zathura
