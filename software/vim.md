[TOC]

# [Overview](https://en.wikipedia.org/wiki/Vim_(text_editor))
Vim (a contraction of Vi IMproved) is a clone of Bill Joy's vi text editor program for Unix. It was written by Bram Moolenaar based on source for a port of the Stevie editor to the Amiga.

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
## Undo - Redo in normal mode
`u`: undo
`Ctrl + r`: redo

# The VIM way
Vim is optimized for repetition. Its efficiency stems from the way it tracks our most recent actions.We can always replay the last change with a single keystroke. We need to learn to craft our actions so that they perform a useful  unit of work when replayed. Mastering this concept is the key to becoming effective with Vim.

## The Dot command
The dot command lets us repeat the last change.
- The last change could be one of many things. A change could act at the level of individual characters, entire lines, or even the whole file.
- From the moment we enter Insert mode until we return to Normal mode, Vim records every keystroke. After making a change such as this, the dot command will replay all keystrokes. For examples: `A;something<Esc>`: this is the last change.
- The dot command is a micro macro

## Don't Repeat Yourself
- Two for the Price of One: many of Vim's single-key commands can be seen as a condensed version of two or more other commands.
| Compound Command | Equivalent in Longhand |
| -                | -                      |
| C                | c$                     |
| s                | cl                     |
| S                | ^C                     |
| I                | ^i                     |
| A                | $a                     |
| o                | A<CR>                  |
| O                | ko                     |
- These all compound command switch form Normal to Insert mode. It helps the dot command.
- Keystrokes pattern: one keystroke to move, another to execute. For example: `j.`.

## Take one step back, then three forward
- Make the motion repeatable:
	+ `f{char}`: look ahead for the next occurrence of the specified character and then move the cursor directly to it if a match is found.
	+ `;`: repeat the last search that the `f` command performed.
- Make the change repeatable:
	+ `s`: deletes the character under the cursor and then enters Insert mode.
- All together: `;.`
	+ `;`: takes us to our next target.
	+ `.`: repeats the last change.

## Act, Repeat, Reverse
| Intent                           | Act                   | Repeat | Reverse |
| -                                | -                     | -      | -       |
| Make a change                    | {edit}                | `.`    | `u`     |
| Scan line for next character     | `f{char}`/`t{char}`   | `;`    | `,`     |
| Scan line for previous character | `F{char}`/`T{char}`   | `;`    | `,`     |
| Scan document for next match     | /pattern`<CR>`        | `n`    | `N`     |
| Scan document for previous match | ?pattern`<CR>`        | `n`    | `N`     |
| Perform substitution             | :s/target/replacement | `&`    | `u`     |
| Execute a sequence of changes    | `qx{change}q`         | `@x`   | `u`     |

## Find and Replace by Hand
- Search without typing: `*` - this executes a search for the word under the cursor at that moment. Go to the next occurrence just by hitting the `n` key.
- Make the change repeatable:
	+ `cw`: deletes to the end of the word and then drops into Insert mode.
- All together: `n.` - `n` go to the next occurrence of the word, `.` repeat the last change.

## Meet the Dot formula
One keystroke to move, one keystroke to execute.

# Modes
## Normal Mode
Normal mode is Vim's natural resting state.

### Chunk your undos
In Vim, we can control the granularity of the undo command. From the moment we enter Insert mode until we return to normal mode, everything we type (or delete) counts as a single change. So we can make the undo command operate on words, sentences, or paragraphs just by moderating our use of the `<Esc>` key.
- Use `<Esc>o` to open a new line instead of `<CR>`, that extra granularity from the undo command.
- Leave Insert mode each complete thought (or sentence).

### Compose Repeatable Change
- `daw`: delete a word, using the `aw` text object instead of a motion.
- Making effective use of the dot command often requires some forethought. If you notice that you have to make the same small change in a handful of places, you can attempt to compose your changes in such a way that they can be repeated with the dot command. Recognizing those opportunities takes practice.

### Use Counts to do simple arithmetic
- `{number}<C-a>`: add number to the current number.
- `{number}<C-x>`: subtract number from the current number.
- `set nrformats=`: treat all numerals as decimal.
- `set nfformats=hex/bin/octal`: treat all numerals as hexadecimal/binary/octal (default=octal).

### Don't count if you can repeat
- `d2w`, `2dw`, `dw.`
- I would rather hit the dot command six times than spend the same time looking ahead in order to reduce the number of keys.
- `c3w`

### Combine and Conquer
#### Operator + Motion = Action
- The `d{motion}` command can operate on a single character `dl`, a complete word `daw`, or an entire paragraph `dap`. The same goes for `c{motion}`, `y{motion}`.

The most common operators:
| Operator | Effect                                            |
| -        | -                                                 |
| `c`      | Change                                            |
| `d`      | Delete                                            |
| `y`      | Yank into register                                |
| `g~`     | Swap case                                         |
| `gu`     | make lowercase                                    |
| `gU`     | Make uppercase                                    |
| `>`      | Shift right                                       |
| `<`      | Shift left                                        |
| `=`      | Autoindent                                        |
| `!`      | Filter {motion} lines through an external program |

- When an operator command is invoked in duplicate, it acts upon the current line. The `gU` command is a special case. We can make it act upon the current line by running either `gUgU` or `gUU`.

#### Extending Vim's Combinatorial Powers
##### Custom Operators Work with Existing Motions
- Tim Pope's `commentary.vim` plugin: this adds a command for commenting and uncommenting lines of code in all languages supported by Vim.
- The commentary command is triggered by `\\{motion}`, which toggles commenting for the specified lines. It's an operator command, so we can combine it with all of the usual motions. `\\ap` will toggle commenting for the current paragraph. `\\G` comments from the current line to the end of the file. `\\\` comments the current line.
- How to create your own custom operators: `:h :map-operator`.

##### Custom Motions Work with existing operators
- Kana Natsuno's `textobj-entire` plugin: it adds two new text objects to Vim: `ie` and `ae`, which act upon the entire file.
- If we wanted to autoindent the entire file using the `=` command, we could run `gg=G` (that is, `gg` to jump to the top of the file and then `=G` to autoindent everything from the cursor position to the end of the file) or `=ae`.
- How to create custom motions: `:h omap-info`

#### Operator-Pending Mode
- When we run the command `dw`, the operator-pending mode lasts during the brief interval between pressing `d` and `w` keys.
- If we think of Vim as a finite-state machine, then Operator-Pending mode is a state that accepts only motion commands. It is activated when we invoke an operator command, and then nothing happens until we provide a motion, which completes the operation. While Operator-Pending mode is active, we can return to normal mode in the usual manner by pressing escape, which aborts the operation.
- Only the operator commands initiate Operator-Pending mode.
- The Operator-Pending mode allows us to create custom operators and motions, which in turn allows us to expand Vim's vocabulary.

## Insert Mode
### Make Corrections Instantly from Insert Mode
| Keystrokes | Effect                                |
| -          | -                                     |
| `<C-h>`    | Delete back one character (backspace) |
| `<C-w>`    | Delete back one word                  |
| `<C-u>`    | Delete back to start of line.         |

### Get back to normal mode
| Keystrokes | Effect                       |
| -          | -                            |
| `<Esc>`    | Switch to Normal mode        |
| `<C-[>`    | Switch to Normal mode        |
| `<C-o>`    | Switch to Insert Normal mode |

- Insert Normal mode: we can fire off a single command, after which we'll be returned to Insert mode immediately.
	+ `<C-o>zz`: the `zz` command redraws the screen with the current line in the middle of the window

### Paste in Insert mode
- `<C-r>{register}`: using when paste a small text less than one line. If you want to paste a register containing multiple lines of text, you should switch to Normal mode and use one of the put commands.
- Remap Caps Lock key to Escape or Ctrl key.

### Do Back-of-the-Envelope Calculations in Place
- Most of Vim's registers contain text either as a string of characters or as entire lines of text. The delete and yank commands allow us to set the contents of a register, while the put command allows us to get the contents of a register by inserting it into the document.
- The expression register is different. It can evaluate a piece of Vim script code and return the result. Here, we can use it like a calculator. Passing it a simple arithmetic expression, such as `1+1`, gives a result of 2. We can use the return value from the expression register just as though it were a piece of text saved in a plain old register.
- The expression register is addressed by the `=` symbol. From Insert mode we can access it by typing `<C-r>=`. This opens a prompt at the bottom of the screen where we can type the expression that we want to evaluate. When done, we hit `<CR>`, and Vim inserts the result at our current position in the document.

### Insert Unusual Characters by Character Code
| Keystrokes            | Effect                                                   |
| -                     | -                                                        |
| `<C-v>{123}`          | Insert character by decimal code                         |
| `<C-v>u{1234}`        | Insert character by hexadecimal code                     |
| `<C-v>{nondigi}`      | Insert nondigit literally                                |
| `<C-k>{char1}{char2}` | Insert character represented by `{char1}{char2}` digraph |

- Digraph: pairs of characters that are easy to remember.
	+ `:h digraphs-default`
	+ `:h digraph-table`

### Overwrite existing text with replace mode
- Replace mode is identical to Insert mode, except that it overwrites existing text in the document.
- Normal mode -> Replace mode: `R` - dealing with the actual characters be saved in a file -> some problems with tab.
- Normal mode -> Virtual Replace mode: `gR` - overwrite characters of screen real estate -> produce fewer surprises, working fine with tab -> recommendation choice.
- Single-shot: Normal mode -> Replace/Virtual Replace mode -> overwrite a single character -> Normal mode: `r{char}` and `gr{char}`

## Visual Mode
- Visual mode allows us to define a selection of text and then operate upon it.
- Vim has three variants of Visual mode involving working with characters, lines, or rectangular blocks of text.

### Grok Visual Mode
- Many of the commands that you are familiar with from Normal mode work just the same in Visual mode.
	+ We can still use `h`, `j`, `k`, `l` as cursor keys.
	+ We can use `f{char}` to jump to a character on the current line and then repeat or reverse the jump with the `;` and `,`.
	+ Search command `/` and `n`/`N` to jump to pattern matches.
- Select mode: resembles the selection mode  in Microsoft Windows. Printable characters cause the selection to be deleted. Vim enters Insert mode, and the typed character is inserted. Not really useful.
- Visual mode -> Select mode: `<C-g>`

### Define a Visual Selection
#### Enabling Visual Modes
| Command | Effect                             |
| -       | -                                  |
| `v`     | Enable character-wise Visual mode  |
| `V`     | Enable line-wise Visual mode       |
| `<C-v>` | Enable block-wise Visual mode      |
| `gv`    | Reselect the last visual selection |

#### Switching Between Visual Modes
| Command               | Effect                               |
| -                     | -                                    |
| `<Esc>` or `<C-[>`    | Switch to Normal mode                |
| `v` or `V` or `<C-v>` | Switch to Normal mode                |
| `v`                   | Switch to character-wise Visual mode |
| `V`                   | Switch to line-wise Visual mode      |
| `<C-v>`               | Switch to block-wise Visual mode     |
| `o`                   | Go to other end of highlighted text  |

### Repeat Line-Wise Visual Commands
- The dot command repeats the change on the same range of text. It is useful to a line-wise selection.
- We should prefer operator commands (e.g. `<gU>{motion}`) over their Visual mode equivalents when working through a repetitive set of changes. Sometimes we need to modify a range of text whose structure is difficult to trace. In these case, Visual mode is the right tool.

### Edit Tabular Data with Visual-Block mode
- Practicing: `<C-v>`, `x`, `.`, `gv`, `r`, `yy`, `p`.

# Files
## Manage Multiple Files
### Track Open Files with the Buffer List
- We can load multiple files during an editing session. Vim lets us manage them using the buffer list.
- Workflow: disk -> read -> buffer - we make changes -> write, update, saveas -> disk.

#### Meet the Buffer List
- `:ls`: gives us a listing of all the buffers that have been loaded into memory.
	+ `%` symbol indicates the current file
	+ `#` symbol represents the alternative file.
	+ `a` character indicates the active file.
	+ `h` character indicates the hidden file.
- `:bnext` or `:bprev`: switch to the next or previous buffer in the list.
- `:bfirst` or `:blast`: jump to the start or end of the list.
- `<C-^>`: toggle between the current and alternate files.
- `:bdelete N1 N2 N3`: delete buffer N1, N2, N3.
- `:N,M bdelete`: delete buffer from N to M.

### Group Buffers into a Collection with the Argument List
- The argument list is easily managed and can be useful for grouping together a collection of files for easy navigation.
- We can run an Ex command on each item in the argument list using the `:argdo` command.
- The argument list represents the list of files that was passed as an argument when we ran the `vim` command.
	+ The `[]` characters indicate which of the files in the argument list is active.
	+ The argument list was a feature of `vi`, whereas the buffer list is an enhancement introduced by Vim.
	+ We can change the contents of the argument list at any time.

#### Populate the Argument List:
- `:args`: print the contents of the argument list.
- `:args {arglist}`: set the contents of the argument list.
	+ The `{arglist}` can include filenames, wildcards, or even the output from a shell command.
	+ Filenames: `:args index.html app.js`
	+ Glob (using wildcards): `:args *.*`, `:args **/*.js`, `:args **/*.*`.
		* `*` symbol will match zero or more characters, but only in the scope of the specified directory.
		* `**` symbol also matches zero or more characters, but it can recurse downward into directories below the specified directory.
		* `?` matches one character
		* `[abc]` match `a`, `b` or `c`.
	+ Output of shell command (backtick expansion): **:args `cat .chapters`**

#### Use the Argument List
- It is the ideal place to group our buffers into a collection.
- With the `:args {arglist}` command, we can clear the argument list and then repopulate it from scratch with a single command.
- We can use `:argdo` to execute the same command on each buffer in the set.

### Manage Hidden Files
- `set hidden`: we can switch between buffer without error messages.
	+ Accept the `:argdo` or `bufdo` to execute

| Command     | Effect                                                                 |
| -           | -                                                                      |
| `:w[rite]`  | Write the contents of the buffer to disk                               |
| `:e[dit]!`  | Read the file from disk back into the buffer (that is, revert changes) |
| `:qa[all]!` | Close all windows, discarding changes without warning (not recommend)  |
| `:wa[all]`  | Write all modified buffers to disk                                     |

### Divide your workspace into split windows
- Vim allows us to view multiple buffers side by side by dividing our workspace into split windows.
- In Vim's terminology, a `window` is a viewport onto a buffer.
	+ We can open multiple windows, each containing the same buffer, or we can load different buffers into each window.

#### Creating Split Windows
- When Vim starts up, it contains a single window.

| Command          | Effect                                                                              |
| -                | -                                                                                   |
| `<C-w>s`         | Split the current window horizontally, reusing the current buffer in the new window |
| `<C-w>v`         | Split the current window vertically, reusing the current buffer in the new window   |
| :sp[lit] {file}  | Split the current window horizontally, loading {file} into the new window           |
| :vsp[lit] {file} | Split the current window vertically, loading {file} into the new window             |

#### Changing the focus between windows
`:h window-move-cursor`

| Command  | Effect                        |
| -        | -                             |
| `<C-w>w` | Cycle between open windows    |
| `<C-w>h` | Focus the window to the left  |
| `<C-w>j` | Focus the window below        |
| `<C-w>k` | Focus the window above        |
| `<C-w>l` | Focus the window to the right |

`<C-w><C-w>` = `<C-w>w`, so on.

#### Closing windows
| Ex command | Normal Command | Effect                                          |
| -          | -              | -                                               |
| :cl[ose]   | `<C-w>c`       | Close the active window                         |
| :on[ly]    | `<C-w>o`       | Keep only the active window, closing all others |

#### Resizing and Rearranging Windows
`:h window-resize`

| Keystrokes  | Buffer Contents                          |
| -           | -                                        |
| `<C-w>=`    | Equalize width and height of all windows |
| `<C-w>_`    | Maximize height of the active window     |
| `[N]<C-w>_` | Set active window height to [N] rows     |

- `<C-w>|`: Maximize width of the active window
- `[N]<C-w>|`: Set active window width to [N] columns

`:h window-moving`

### Organize your window layouts with tab pages
- When we open a file using the `:edit` command, Vim doesn't automatically create a new tab. Instead, it creates a new buffer and loads it into the current window. Vim keeps track of the set of files that are open using the buffer list.
- We can use tab pages to organize split windows into a collection of workspaces. A tab page is a container that can hold a collection of windows.

#### How to use tabs
- Vim's tab pages can be used to partition work into different workspaces. They have more in common with the virtual desktops in Linux than they do with the tabbed interface of most other text editors.
- The `:lcd{path}` command lets us set the working directory locally for the current window. If we create a new tab page and then use the `:lcd` command to switch to another directory, we can then comfortably scope each tab page to a different project.
- Note that `:lcd` applies locally to the current window, not to the current tab page. If we have a tab page containing two or more split windows, we could set the local working directory for all of them by running `:windo lcd {path}`.

#### Opening and Closing Tabs
| Command                 | Effect                                            |
| -                       | -                                                 |
| `:tabe[dit] {filename}` | Open `{filename}` in a new tab                    |
| `<C-w>T`                | Move the current window into its own tab          |
| `tabc[lose]`            | Close the current tab page and all of its windows |
| `tabo[nly]`             | Keep the active tab page, closing all others      |

#### Switching between tabs
| Ex Command       | Normal Command | Effect                          |
| -                | -              | -                               |
| `:tabn[ext] {N}` | `{N}gt`        | Switch to tab page number {N}   |
| `:tabn[ext]`     | `gt`           | Switch to the next tab page     |
| `:tabp[revious]` | `gT`           | Switch to the previous tab page |

#### Rearranging Tabs
- `:tabmove [N]`
	+ [N] = 0: move to the beginning
	+ omit [N]: move to the end

## Open Files and Save Them to Disk
### Open a file by its filepath using ":edit"
#### Open a File relative to the current working directory
- When Vim is launched, it adopts the same working directory that was active in the shell.
	+ `:pwd`: print working directory
	+ `:edit {file}`: command can accept a filepath relative to the working directory. `:edit lib/framework.js`

#### Open a File Relative to the Active File Directory
- `:edit %:h<Tab>`: expand to the full path of the current file's directory
- Mapping:

```
" Easy Expansion of the Active File Directory
let mapleader=','
" cnoremap <expr> %% getcmdtype() == ':' ? expand('%:h').'/' : '%%'
cnoremap %% <C-R>=fnameescape(expand('%:h')).'/'<cr>
map <leader>ew :e %%
map <leader>es :sp %%
map <leader>ev :vsp %%
map <leader>et :tabe %%
```
- Now we can use `%%` to expand the current file's directory in any ex command such as `:write`, `:saveas`, `:read`.

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
