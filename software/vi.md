[TOC]

# Overview

Was written by C in 1976 by Bill Joy. Simple and clear. Do not have
multiple undo, multiple screen or syntax highlighting.

VI has two mode: command mode and insert mode. Command mode use for run
command in VI such copy, paste, etc. Insert mode use for type text.
Change mode by press `ESC`.

[Source Code](http://ex-vi.cvs.sourceforge.net/viewvc/ex-vi/ex-vi/)

- http://www.cs.colostate.edu/helpdocs/vi.html
- http://www.cs.rit.edu/~cslab/vi.html
- http://www.yolinux.com/TUTORIALS/LinuxTutorialAdvanced_vi.html
- http://www.atmos.albany.edu/deas/atmclasses/atm350/vi_cheat_sheet.pdf
- http://www.lagmonster.org/docs/vi.html
- https://www.ccsf.edu/Pub/Fac/vi.html

# Tutorials

Start `vi`:
- `vi filename`
- `vi -r filename`: recover filename that was being edited when system
  crashed.

Exit `vi`:
- `:x<Enter>` : quit vi, writing out modified file to file named in
  original invocation
- `:wq<Enter>` : same `:x<Enter>`
- `:q<Enter>` : quit vi
- `:q!<Enter>` : quit vi even though latest changes have not been saved
  for this vi call

## Moving the cursor


## Screen manipulation



## Edit text


## Other

### Search text

- `/string`	search forward for occurrence of string in text
- `?string`	search backward for occurrence of string in text
- `n`	move to next occurrence of search string
- `N`	move to next occurrence of search string in opposite direction

### Determining line numbers

- `:.=`	returns line number of current line at bottom of screen
- `:=`	returns the total number of lines at bottom of screen
- `^g`    provides the current line number, along with the total number
  of lines, in the file at the bottom of the screen


## Saving and Reading Files

(the line with cursor)
- `:w<Return>`	write current contents to file named in original vi call
- `:w newfile<Return>`    write current contents to a new file named
  newfile
- `:12,35w smallfile<Return>` write the contents of the lines numbered
  12 through 35 to a new file named smallfile
- `:r filename<Return>`   read file named filename and insert after
  current line
- `:w! prevfile<Return>`  write current contents over a pre-existing
  file named prevfile
