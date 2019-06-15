[TOC]

# [Overview](https://en.wikipedia.org/wiki/Vim_(text_editor))

Vim (a contraction of Vi IMproved) is a clone of Bill Joy's vi text
editor program for Unix. It was written by Bram Moolenaar based on
source for a port of the Stevie editor to the Amiga.

## History

Initial release in November 1991.

## [Help][2]

- `:help` help facility built-in
- `vimtutor` : basic commands tutorials
- `:h key-notation`: these names for keys are used in the documentation.

### Learn to use help

- `:h <patt>` then press <C-D> to list all topics that contain <patt>
- `:h <patt>` the Tab to scroll through topics that start with <patt>
- `<C-]>` to follow the link
- `<C-o>`: previous location, `<C-i>`: next location
- `:helpgrep \csearch.\{,12}file`
    + `\c` case insensitive
    + the pattern finds `search` then up to 12 characters followed by
        `file`
    + the results are loaded into quickfix list.

```help
| Prefix | Example     | Context                                         |
|--------|:------------|-------------------------------------------------|
| v_     | :h v_r      | visual mode                                     |
| i_     | :h i_CTRL-W | insert mode                                     |
| c_     | :h c_CTRL-R | ex command line                                 |
| /      | :h /\r      | search pattern (in this case, :h \r also works) |
| '      | :h 'ro'     | option                                          |
| -      | :h -r       | Vim argument (starting Vim)                     |
```

The following mappings simplify navigation when viewing help:

- Press Enter to jump to the subject (topic) under the cursor.
- Press Backspace to return from the last jump.
- Press s to find the next subject, or S to find the previous subject.
- Press o to find the next option, or O to find the previous option.

```vim
" Create file ~/.vim/ftplugin/help.vim
nnoremap <buffer> <CR> <C-]>
nnoremap <buffer> <BS> <C-T>
nnoremap <buffer> o /'\l\{2,\}'<CR>
nnoremap <buffer> O ?'\l\{2,\}'<CR>
nnoremap <buffer> s /\|\zs\S\+\ze\|<CR>
nnoremap <buffer> S ?\|\zs\S\+\ze\|<CR>
```



## Features and improvements over vi

### Customization

Part of Vim's power is that it can be extensively customized.
- Change basic interface
- Define personalized key mappings
- Abbreviations to automate sequences of keystrokes
- Call internal or user defined functions

Plugins available that will extend or add new functionality to Vim.
- Vim's internal scripting language - vimscript (viml)
- Lua, Perl, Python, Racket, Ruby, and Tcl

### Search and replace

- Change each "foo" to "bar" in the current line: `:s/foo/bar/g` and
  have confirm : `:s/foo/bar/gc`
- Change each "foo" to "bar" in all the lines: `:%s/foo/bar/g` and have
  confirm: `:%s/foo/bar/gc`
- Change each "foo" to "bar" for all lines from line 5 to line 12:
  `:5,12s/foo/bar/gc`

### Copy and paste

- Copy to clipboard
    + Using registers
        * X11's primary register: `"*y`, `"*p`
        * X11's clipboard register: `"+y`, `"+p`
- Configuration at `.vimrc` : `xnoremap p pgvy` it mean *p* will replay
  with *pgvy*, *p* to paste and *gv* to re-select what was originally
  selected, *y* to copy it again.
- Paste multiple copy: *<number>p* e.g: *30p* to paste 30 time of copy
  text.

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
- [Thoughtbot Tutorials](https://upcase.com/vim)
- [vimcast](http://vimcasts.org/)

### Books

- [Books](http://iccf-holland.org/click5.html)
- Practical Vim - 2nd edition
- [Modern Vim](https://pragprog.com/book/modvim/modern-vim)
- Learn Vimscript the Hard Way
    + http://learnvimscriptthehardway.stevelosh.com/

# Getting started

- 7 habits of effective text editing

## Edit a file

### Move around quickly

- Disable key repeat, arrow keys, backspace in insert mode
- If you know the word that you want to find
    + Search the current word `*` `/<word>` to search the word
- If you don't know the word
    + First, identify the location in the file: top, middle, bot
        * Using page up, down
    + Second, if the location in the screen area, jump to the place
        using relative line number
        * `H`, `M`, `L`: go to the top, middle, bottom of the screen
    + In the line, use `f<char>` to mark the character's position
      (including the character) and `t<char>` to mark the position right
      before the character
- `%` jump from open item to matching item
- `[{` back to the starting `{`
- `]}` to the closing `}`
- `gd` from the use to the declaration of a variable
- `tpope/vim-rsi`: readline Emacs' mappings
    + `<C-e>`: to the end of the line
    + `<C-f>`: forward one character

### Don't type it twice

- `:s`: substitute
- `*`: find word and `cw`
    + `n` go to next item in the search results
- `.`: repeat the change
    + `m`: mark the location to come back later
- `<C-n>`: auto complete
- `qa` start recording a macro into register `a` (total 26 registers)
    + hit `q` again to stop recording
    + apply the macro by typing `@a`
    + should use commands to move over text objects (words, sentences,
        etc.) instead of characters
- Snippets

### Fix it when it's wrong

- Correct mistakes using spell check
    + `:setlocal spell spelllang=en_us`
    + `:h spell`

```vim
" A mapping to quickly correct the previous spelling error
imap <C-l> <C-g>u<Esc>[s1z=`]a<C-g>u
```

### Work with multiple files

- Using a fuzzy finder to quickly find files and search the file content
- `[I`: show a list of matched for the function name under the cursor in
    included files.
- Using preview-tag mechanism, an open special preview window.

### Text is structured

- edit-compile-fix cycle `:make` command
    + which starts your compilation, catches the errors it produces and
      lets you jump to the error locations to fix the problems

# Basic Usage

## Undo - Redo in normal mode

`u`: undo
`Ctrl + r`: redo

# The VIM way

Vim is optimized for repetition. Its efficiency stems from the way it
tracks our most recent actions.We can always replay the last change with
a single keystroke. We need to learn to craft our actions so that they
perform a useful  unit of work when replayed. Mastering this concept is
the key to becoming effective with Vim.

## The Dot command

The dot command lets us repeat the last change.
- The last change could be one of many things. A change could act at the
  level of individual characters, entire lines, or even the whole file.
- From the moment we enter Insert mode until we return to Normal mode,
  Vim records every keystroke. After making a change such as this, the
  dot command will replay all keystrokes. For examples:
  `A;something<Esc>`: this is the last change.
- The dot command is a micro macro

## Don't Repeat Yourself

- Two for the Price of One: many of Vim's single-key commands can be
  seen as a condensed version of two or more other commands.

| Compound Command | Equivalent in Longhand |
|------------------|------------------------|
| C                | c$                     |
| s                | cl                     |
| S                | ^C                     |
| I                | ^i                     |
| A                | $a                     |
| o                | A<CR>                  |
| O                | ko                     |

- These all compound command switch form Normal to Insert mode. It helps
  the dot command.
- Keystrokes pattern: one keystroke to move, another to execute. For
  example: `j.`.

## Take one step back, then three forward

- Make the motion repeatable:
    + `f{char}`: look ahead for the next occurrence of the specified
      character and then move the cursor directly to it if a match is
      found.
    + `;`: repeat the last search that the `f` command performed.
- Make the change repeatable:
    + `s`: deletes the character under the cursor and then enters Insert
      mode.
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

- Search without typing: `*` - this executes a search for the word under
  the cursor at that moment. Go to the next occurrence just by hitting
  the `n` key.
- Make the change repeatable:
    + `cw`: deletes to the end of the word and then drops into Insert
      mode.
- All together: `n.` - `n` go to the next occurrence of the word, `.`
  repeat the last change.

## Meet the Dot formula

One keystroke to move, one keystroke to execute.

# Modes

## Normal Mode

Normal mode is Vim's natural resting state.

### Chunk your undos

In Vim, we can control the granularity of the undo command. From the
moment we enter Insert mode until we return to normal mode, everything
we type (or delete) counts as a single change. So we can make the undo
command operate on words, sentences, or paragraphs just by moderating
our use of the `<Esc>` key.
- Use `<Esc>o` to open a new line instead of `<CR>`, that extra
  granularity from the undo command.
- Leave Insert mode each complete thought (or sentence).

### Compose Repeatable Change

- `daw`: delete a word, using the `aw` text object instead of a motion.
- Making effective use of the dot command often requires some
  forethought. If you notice that you have to make the same small change
  in a handful of places, you can attempt to compose your changes in
  such a way that they can be repeated with the dot command. Recognizing
  those opportunities takes practice.

### Use Counts to do simple arithmetic

- `{number}<C-a>`: add number to the current number.
- `{number}<C-x>`: subtract number from the current number.
- `set nrformats=`: treat all numerals as decimal.
- `set nfformats=hex/bin/octal`: treat all numerals as
  hexadecimal/binary/octal (default=octal).

### Don't count if you can repeat

- `d2w`, `2dw`, `dw.`
- I would rather hit the dot command six times than spend the same time
  looking ahead in order to reduce the number of keys.
- `c3w`

### Combine and Conquer

#### Operator + Motion = Action

- The `d{motion}` command can operate on a single character `dl`, a
  complete word `daw`, or an entire paragraph `dap`. The same goes for
  `c{motion}`, `y{motion}`.

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

- When an operator command is invoked in duplicate, it acts upon the
  current line. The `gU` command is a special case. We can make it act
  upon the current line by running either `gUgU` or `gUU`.

#### Extending Vim's Combinatorial Powers

##### Custom Operators Work with Existing Motions

- Tim Pope's `commentary.vim` plugin: this adds a command for commenting
  and uncommenting lines of code in all languages supported by Vim.
- The commentary command is triggered by `gc{motion}`, which toggles
  commenting for the specified lines. It's an operator command, so we
  can combine it with all of the usual motions. `gcap` will toggle
  commenting for the current paragraph. `gcG` comments from the current
  line to the end of the file. `gcc` comments the current line.
- How to create your own custom operators: `:h :map-operator`.

##### Custom Motions Work with existing operators

- Kana Natsuno's `textobj-entire` plugin: it adds two new text objects
  to Vim: `ie` and `ae`, which act upon the entire file.
- If we wanted to autoindent the entire file using the `=` command, we
  could run `gg=G` (that is, `gg` to jump to the top of the file and
  then `=G` to autoindent everything from the cursor position to the end
  of the file) or `=ae`.
- How to create custom motions: `:h omap-info`

#### Operator-Pending Mode

- When we run the command `dw`, the operator-pending mode lasts during
  the brief interval between pressing `d` and `w` keys.
- If we think of Vim as a finite-state machine, then Operator-Pending
  mode is a state that accepts only motion commands. It is activated
  when we invoke an operator command, and then nothing happens until we
  provide a motion, which completes the operation. While Operator-
  Pending mode is active, we can return to normal mode in the usual
  manner by pressing escape, which aborts the operation.
- Only the operator commands initiate Operator-Pending mode.
- The Operator-Pending mode allows us to create custom operators and
  motions, which in turn allows us to expand Vim's vocabulary.

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

- `<C-r>{register}`: using when paste a small text less than one line.
  If you want to paste a register containing multiple lines of text, you
  should switch to Normal mode and use one of the put commands.
- Remap Caps Lock key to Escape or Ctrl key
    + Put this line in .xinitrc file: `setxkbmap -option caps:escape`
    + Caps Lock as Ctrl: `setxkbmap -option ctrl:nocaps`

### Do Back-of-the-Envelope Calculations in Place

- Most of Vim's registers contain text either as a string of characters
  or as entire lines of text. The delete and yank commands allow us to
  set the contents of a register, while the put command allows us to get
  the contents of a register by inserting it into the document.
- The expression register is different. It can evaluate a piece of Vim
  script code and return the result. Here, we can use it like a
  calculator. Passing it a simple arithmetic expression, such as `1+1`,
  gives a result of 2. We can use the return value from the expression
  register just as though it were a piece of text saved in a plain old
  register.
- The expression register is addressed by the `=` symbol. From Insert
  mode we can access it by typing `<C-r>=`. This opens a prompt at the
  bottom of the screen where we can type the expression that we want to
  evaluate. When done, we hit `<CR>`, and Vim inserts the result at our
  current position in the document.

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

- Replace mode is identical to Insert mode, except that it overwrites
  existing text in the document.
- Normal mode -> Replace mode: `R` - dealing with the actual characters
  be saved in a file -> some problems with tab.
- Normal mode -> Virtual Replace mode: `gR` - overwrite characters of
  screen real estate -> produce fewer surprises, working fine with tab
  -> recommendation choice.
- Single-shot: Normal mode -> Replace/Virtual Replace mode -> overwrite
  a single character -> Normal mode: `r{char}` and `gr{char}`

## Visual Mode

- Visual mode allows us to define a selection of text and then operate
  upon it.
- Vim has three variants of Visual mode involving working with
  characters, lines, or rectangular blocks of text.

### Grok Visual Mode

- Many of the commands that you are familiar with from Normal mode work
  just the same in Visual mode.
    + We can still use `h`, `j`, `k`, `l` as cursor keys.
    + We can use `f{char}` to jump to a character on the current line
      and then repeat or reverse the jump with the `;` and `,`.
    + Search command `/` and `n`/`N` to jump to pattern matches.
- Select mode: resembles the selection mode  in Microsoft Windows.
  Printable characters cause the selection to be deleted. Vim enters
  Insert mode, and the typed character is inserted. Not really useful.
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

- The dot command repeats the change on the same range of text. It is
  useful to a line-wise selection.
- We should prefer operator commands (e.g. `<gU>{motion}`) over their
  Visual mode equivalents when working through a repetitive set of
  changes. Sometimes we need to modify a range of text whose structure
  is difficult to trace. In these case, Visual mode is the right tool.

### Edit Tabular Data with Visual-Block mode

- Practicing: `<C-v>`, `x`, `.`, `gv`, `r`, `yy`, `p`.

# Files

## Manage Multiple Files

### Track Open Files with the Buffer List

- We can load multiple files during an editing session. Vim lets us
  manage them using the buffer list.
- Workflow: disk -> read -> buffer - we make changes -> write, update,
  save as -> disk.

#### Meet the Buffer List

- `:ls`: gives us a listing of all the buffers that have been loaded
  into memory.
    + `%` symbol indicates the current file
    + `#` symbol represents the alternative file.
    + `a` character indicates the active file.
    + `h` character indicates the hidden file.
- `:bnext` or `:bprev`: switch to the next or previous buffer in the
  list.
- `:bfirst` or `:blast`: jump to the start or end of the list.
- `<C-^>`: toggle between the current and alternate files.
- `:bdelete N1 N2 N3`: delete buffer N1, N2, N3.
    + `bd` or `bdelete` is used to close buffers. If the buffers are
        changed, it will fail.
- `:N,M bdelete`: delete buffer from N to M.

### Group Buffers into a Collection with the Argument List

- The argument list is easily managed and can be useful for grouping
  together a collection of files for easy navigation.
- We can run an Ex command on each item in the argument list using the
  `:argdo` command.
- The argument list represents the list of files that was passed as an
  argument when we ran the `vim` command.
    + The `[]` characters indicate which of the files in the argument
      list is active.
    + The argument list was a feature of `vi`, whereas the buffer list
      is an enhancement introduced by Vim.
    + We can change the contents of the argument list at any time.

#### Populate the Argument List:

- `:args`: print the contents of the argument list.
- `:args {arglist}`: set the contents of the argument list.
    + The `{arglist}` can include filenames, wildcards, or even the
      output from a shell command.
    + Filenames: `:args index.html app.js`
    + Glob (using wildcards): `:args *.*`, `:args **/*.js`, `:args
      **/*.*`.
        * `*` symbol will match zero or more characters, but only in the
          scope of the specified directory.
        * `**` symbol also matches zero or more characters, but it can
          recurse downward into directories below the specified
          directory.
        * `?` matches one character
        * `[abc]` match `a`, `b` or `c`.
    + Output of shell command (backtick expansion): **:args `cat .chapters`**

#### Use the Argument List

- It is the ideal place to group our buffers into a collection.
- With the `:args {arglist}` command, we can clear the argument list and
  then repopulate it from scratch with a single command.
- We can use `:argdo` to execute the same command on each buffer in the
  set.

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

- Vim allows us to view multiple buffers side by side by dividing our
  workspace into split windows.
- In Vim's terminology, a `window` is a viewport onto a buffer.
    + We can open multiple windows, each containing the same buffer, or
      we can load different buffers into each window.

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

- When we open a file using the `:edit` command, Vim doesn't
  automatically create a new tab. Instead, it creates a new buffer and
  loads it into the current window. Vim keeps track of the set of files
  that are open using the buffer list.
- We can use tab pages to organize split windows into a collection of
  workspaces. A tab page is a container that can hold a collection of
  windows.

#### How to use tabs

- Vim's tab pages can be used to partition work into different
  workspaces. They have more in common with the virtual desktops in
  Linux than they do with the tabbed interface of most other text
  editors.
- The `:lcd{path}` command lets us set the working directory locally for
  the current window. If we create a new tab page and then use the
  `:lcd` command to switch to another directory, we can then comfortably
  scope each tab page to a different project.
- Note that `:lcd` applies locally to the current window, not to the
  current tab page. If we have a tab page containing two or more split
  windows, we could set the local working directory for all of them by
  running `:windo lcd {path}`.

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

### Open a file by its filepath using `:edit`

#### Open a File relative to the current working directory

- When Vim is launched, it adopts the same working directory that was
  active in the shell.
    + `:pwd`: print working directory
    + `:edit {file}`: command can accept a filepath relative to the
      working directory. `:edit lib/framework.js`

#### Open a File Relative to the Active File Directory

- `:edit %:h<Tab>`: expand to the full path of the current file's
  directory
- Mapping:

```vim
" Easy Expansion of the Active File Directory
let mapleader=','
" cnoremap <expr> %% getcmdtype() == ':' ? expand('%:h').'/' : '%%'
cnoremap %% <C-R>=fnameescape(expand('%:h')).'/'<cr>
map <leader>ew :e %%
map <leader>es :sp %%
map <leader>ev :vsp %%
map <leader>et :tabe %%
```

- Now we can use `%%` to expand the current file's directory in any ex
  command such as `:write`, `:saveas`, `:read`.

### Open a file by Its Filename Using `:find`

- The `:find` command allows us to open a file by its name without
  having to provide a fully qualified path. To exploit this feature, we
  first have to configure the `path` setting.

#### Configure the `path`

- The `path` option allows us to specify a set of directories inside of
  which Vim will search when the `:find` command is invoked.
    + show current path: `:set path?`
    + `:set path+=app/**`
    + see `:h path` and `:h file-searching`

#### Use `:find` to look up Files by name

- Now that we've configured our `path`, we can open files in the
  directories we specified by providing just their name.
- `:find {some_chars}<Tab>`: tab-completion shows up.
- Configure `wildmod` and `wildmenu` to change the tab-completion
  behavior.  `:h wildmode`, `:h wildmenu`

### Explore the File System with netrw

- The netrw plugin, included in the Vim distribution, allows us to
  explore the file system.
- The netrw plugin comes as standard with the Vim distribution, so we
  don't have to install anything, but we do need to make sure that Vim
  is configured to load plugins.

```vim
set nocompatible
filetype plugin on
```

#### Meet netrw - Vim's Native File Explorer

- Open the File Explorer

| Ex Command  | Shorthand | Effect                                                    |
| -           | -         | -                                                         |
| `:edit .`   | `:e.`     | Open file explorer for current working directory          |
| `:Explore`  | `:E`      | Open file explorer for the directory of the active buffer |
| `:Sexplore` | `:Se`     | Open the file explorer in a horizontal split window       |
| `:Vexplore` | `:Ve`     | Open the file explorer in a vertical split window         |

- Working with split windows: `<C-^>` switch back and forth between the
  buffer and the file explorer.

#### Doing more with netrw

- Create new files: `:h netrw-%`
- Create new directories: `:h netrw-d`
- Rename existing ones: `:h netrw-rename`
- Delete files: `:h netrw-del`
- Watch [episode 15 of Vimcasts][1]
- Read and write files across a network: `:h netrw-ref`

# Tips and Tricks

## List all filetypes in Vim

```sh
# cd to vim directory
cd $(vim -Nesc '!echo $VIMRUNTIME' -c qa)

# list all filetypes
find syntax ftplugin -iname '*.vim' -exec basename -s .vim {} + | sort -u
```


## Inspecting Vim's Variables

- `:echo <variable_name>`
- `:echo g:Something`

## Open help in another split pane

- `:vert help`
    + `:vert h`
    + `:vert topleft h`
    + `:vert botright h`

## Convert existing tabs to spaces

- `:retab`

## Remove search highlights until the next search

`:noh`


## Jump Back To Previous or Last Cursor Position

```help

[a] '. : Jump to last modification line.

[b] `. : Jump to exact spot in last modification line

[c] CTRL-O : Retrace your movements in file in backwards.

[d] CTRL-I : Retrace your movements in file in forwards.
```

## Better colorscheme and looking for vim, iterm2, tmux

- https://web.archive.org/web/20190121063455/https://medium.com/@dubistkomisch/how-to-actually-get-italics-and-true-colour-to-work-in-iterm-tmux-vim-9ebe55ebc2be

### configure terminfo

- Create a file `xterm-256color-italic.terminfo`

```sh
xterm-256color-italic|xterm with 256 colors and italic,
  sitm=\E[3m, ritm=\E[23m,
  use=xterm-256color,
```

- Create a file `tmux-256color.terminfo`

```sh
tmux-256color|tmux with 256 colors,
  ritm=\E[23m, rmso=\E[27m, sitm=\E[3m, smso=\E[7m, Ms@,
  khome=\E[1~, kend=\E[4~,
  use=xterm-256color, use=screen-256color,
```

- Install terminfos

```sh
$ tic -x xterm-256color-italic.terminfo
$ tic -x tmux-256color.terminfo
```

### Configure iTerm2

Go to Preferences > Profiles > Default.

Make sure Text > Italic text allowed is checked.

Set Terminal > Report Terminal Type to xterm-256color-italic.

This essentially sets the value of the environment variable TERM, which
you could also set in your ~/.bashrc etc, depending on how you want to
store your settings.

### Configure tmux

Add this to your ~/.tmux.conf:

```vim
set -g default-terminal 'tmux-256color'
set -as terminal-overrides ',xterm*:Tc:sitm=\E[3m'
```

This again sets TERM inside tmux. The second line is even more important
though: Tc allows vim to enable true colors, and sitm allows the same
with italics.



## Configure the Cursor

- http://vim.wikia.com/wiki/Change_cursor_shape_in_different_modes
- http://vim.wikia.com/wiki/Configuring_the_cursor

## Reformatting and Indentation

```help
V=  - select text, then reformat with =
=   - will correct alignment of code
==  - one line;
gq  - reformat paragraph
```

```help
>>   Indent line by shiftwidth spaces
<<   De-indent line by shiftwidth spaces
5>>  Indent 5 lines
5==  Re-indent 5 lines

>%   Increase indent of a braced or bracketed block (place cursor on brace first)
=%   Reindent a braced or bracketed block (cursor on brace)
<%   Decrease indent of a braced or bracketed block (cursor on brace)
]p   Paste text, aligning indentation with surroundings

=i{  Re-indent the 'inner block', i.e. the contents of the block
=a{  Re-indent 'a block', i.e. block and containing braces
=2a{ Re-indent '2 blocks', i.e. this block and containing block

>i{  Increase inner block indent
<i{  Decrease inner block indent
```

## [Accessing the system clipboard](http://vim.wikia.com/wiki/Accessing_the_system_clipboard)

## [Fix meta key in terminal](http://stackoverflow.com/questions/6778961/alt-key-shortcuts-not-working-on-gnome-terminal-with-vim)

## [Moving lines up and down](http://vim.wikia.com/wiki/Moving_lines_up_or_down)

## [Work with multiple files](http://stackoverflow.com/questions/53664/how-to-effectively-work-with-multiple-files-in-vim)

## Show hidden characters like carriage return and linefeed

`vim -b <file>`: show carriage return

`:set list`: to show linefeed

- `:h listchars`
    + `listchars=eol:¬,tab:▸-,trail:·,space:·`

# Tuning Vim

## Vim script

Vim script (`viml`) is the scripting language built into Vim. Based on
the ex editor language of the original vi editor.

Vim script files are stored in plain text format and the file name
extension is `.vim`.

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
- [color names](https://codeyarns.com/2011/07/29/vim-chart-of-color-names/)
- Change cursor line colors
    + `highlight CursorLine ctermbg=DarkBlue`
    + ctermfg, guifg, guibg
- Colorscheme:
    + `:colorscheme delek` or `:colo delek`
    + monokai
        * https://github.com/phanviet/vim-monokai-pro
        * https://github.com/patstockwell/vim-monokai-tasty
- `:syntax on`
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

- https://vimawesome.com/

### vim-markdown

- Disable folding
    + `let g:vim_markdown_folding_disabled = 1`

### vim-sneak

- `s<char><char>`: jump forward to the matches 2 characters
- `;`: next match, `3;`: skip to the third match
- `<C-o>`: back to the starting point
- `s<Enter>` repeat the last sneak-search
- `S` search backwards
- `3dzqt`: delete to the third instance of `qt`
    + `.` to repeat the whole operation
    + `2.` to repeat twice
    + `d;` delete up to the next match
    + `4d;` delete up to the fourth next match
- `yszxy]` surround brackets up to xy
    + `.` to repeat
- `gUz\}` uppercase from the cursor to the next instant of `\}`
    + `.` to repeat

### vim-scriptease

- The plugin helps making plugins
- `:Verbose <command>`: open a preview window to capture command's
    results

### fugitive-vim

#### Commands ####

- `:Git` Run an arbitrary git command. Similar to :!git [args] but chdir
    to the repository tree first.
- `:Gstatus` or `:G`: bring up a summary window similar git-status
    + `s`: stage (add) the file or hunk under the cursor
    + `u`: unstage (reset) the file or hunk under the cursor
    + `-`: stage or unstage
    + `<C-N>` or `J`: skip to the next file or hunk
    + `<C-P>` or `K`: skip to the previous file or hunk
    + `X`: discard the change under the cursor
        * Use `:messages` to see the message again
    + `=`: toggle inline diff of the file under the cursor
    + `<`: insert an inline diff of the file under the cursor
    + `>`: remove the inline diff of the file under the cursor
    + `i`: on untracked files, git-add, otherwise, move to the next
        hunk, expanding inline diffs automatically.
    + `dd`: perform a `:Gdiff` on the file under the cursor
    + `ds`: split horizontally diff
    + `dv`: split vertically
    + `P`: invoke `:Git add --patch` or `reset --path` on the file
    + `cc`: create a commit
    + `ca`: amend the last commit and edit the message
    + `ce`: Amend the last commit without editing the message
    + `cw`: reword the last commit
    + `cvc`: create a commit with -v (new tab)
    + `cva`: amend the last commit with -v (new tab)
    + `gq`: close the status buffer
    + `R`: reload the status buffer
    + `.`: start a `:` command line with the file path under the cursor
        prepopulated.
    + `g?`: open the help file
- `:Gcommit`: open a split window to obtain a commit message
    + `:Gcommit -v`: open a new tab instead of a split window
    + `:Gcommit % -v`: stage the change of this file and open a new tab
        to obtain a commit message
    + `:Gcommit -m <message>`: commit the staged change with the
        <message>
    + `:Gcommit % -m <message>`: stage the change and commit with the
        <message>
- `:Gpull`, `:Gpush`: results are loaded into the quickfix list
    + Using `:copen` to open the quickfix list
- `:Glog`: load all the revision of this file into the quickfix list.
    + `:Glog -- %`: load the commit history of this file into the
        quickfix list
    + `:Glog --`: complete the commit history of all files
    + `:Glog`: all revisions of this file
    + `:Glog -10`: the last ten revisions
    + `:Glog -10 --revese`: the first ten revisions
    + `:Glog -1 --until=yesterday`: the last revision this file that was
        checked in before midnight
    + `:Glog --grep=findme --`: search <findme> in all commit messages
    + `:Glog --grep=findme -- %`
    + `:Glog -Sfindme --`: search <findme> in the diff
    + `:Glog -Sfindme -- %`
- `:Gedit [fugitive-object]`
    + `:%`: this file in the git index
- `:Gread [object]`: empty the buffer and read a fugitive-object
    + `:Gread`: similar to git-checkout
- `:Gwrite`: write to the current file's path and stage the results
    + similar to git-add
- `:Gdiff [object]`: perform a vimdiff against the given file, or if a
    commit, the current file in that commit.
    + `:Gdiff`: the version in the index is used
    + `:h vimdiff` to learn more about vimdiff
    + `:Gsdiff`: split horizontally
    + `:Gvdiff`: split vertically
- `:Gmove {destination}`: git-mv
- `:Gremove`: git-rm
- `:Gblame [flags]`: run git-blame on this file and open the results in
    a scroll bound vertical split.
    + g?  : show this help
    + A   :  resize to end of author column
    + C   : resize to end of commit column
    + D   : resize to end of date/time column
    + q   : close blame and return to blamed window
    + gq  : q, then |:Gedit| to return to work tree version
    + <CR>: q, then open commit
    + o   : open commit in horizontal split
    + O   : open commit in new tab
    + p   : open commit in preview window
    + -   : reblame at commit
    + ~   : reblame at [count]th first grandparent
    + P   : reblame at [count]th parent (like HEAD^[count])
- `:Gbrowse`: open the current file, blob, tree, commit, or tag in your
    browser at the upstream hosting provider.
    + `https://github.com/tpope/vim-rhubarb>`: GitHub support
- `:Ggrep <findme>` search for <findme> in working copy files
    + `:Ggrep --cached <findme>` search in index
    + `:Ggrep <findme> <branchname>`
    + `:Ggrep <findme> <tagname>`
    + `:Ggrep <findme> <SHA>`

#### Mappings ####

```vim
"""" vim-fugitive mapping
" Using cmdline for other tasks: move, delete, stash, push, pull

" Add all files
nmap <Leader>ga :Git add .<CR>

nmap <Leader>gb :Gblame<CR>
nmap <Leader>gs :Gstatus<CR>

" Commit after adding
nmap <Leader>gc :Gcommit -v<CR>

" Add the file then commit it
" Take advantage of autocomplete in writing commit message
" Hit Ctrl-n to autocomplete the word
nmap <Leader>gC :Gcommit % -v<CR>

" Commit without invoking an editor
nmap <Leader>gg :Gcommit % -m ""<Left>

" Stage the current hunk and commit it
nmap <Leader>gh ,hs,gc

" Mydiff is a wrapper around Gdiff
nmap <Leader>gd :Mydiff<CR>

" Edit a fugitive-object, e.g. :% is the current file in the git index
" :h fugitive-object to learn more
" This map is to edit the current file in the git index
nmap <Leader>ge :Gedit<CR>

" Similar to git-checkout on a work tree file
nmap <Leader>gr :Gread<CR>

" Similar to git-add on a work tree file
nmap <Leader>gw :Gwrite<CR>

" Load this file's commit history into the quickfix list
" :copen to open the quickfix list
nmap <Leader>gl :Glog -- %<CR><CR>:copen<CR>

" List all commit history
nmap <Leader>gL :exe ':!cd ' . expand('%:p:h') . '; git lap'<CR>

" Rename the file, the new location is relative to the current file path
nmap <Leader>gm :Gmove<Space>

" Delete the file
nmap <Leader>gM :Gremove<CR>

nmap <Leader>gp :Gpush<CR>
nmap <Leader>gl :Gpull<CR>
```


#### Work flows ####

- Modify the file
    + Commit hunks or commit the whole file
    + If you can, commit without invoke an editor is faster
- Merging
    + 3-way merge: target branch, working copy, merge branch
    + from working copy version
        * `:diffget <target/merge>` to get the change
    + from target or merge branch version
        * `:diffput` or `dp` to put the change to the working copy
    + after done with fixing changes, use `:Gwrite` in the working copy
        windows to close other buffers and keep the working copy buffer
        and stage the changes
        * We can use `:Gwrite!` in the target or merge window to keep
            the whole changes in that version, stage the changes, close
            all the buffers except the working copy
    + commit the changes
- Browsing git objects
    + Reading a file any branch: `:Gedit branch:path/to/file`
        * can use tab for auto complete branch name and file path
        * `%` current file path
    + Git objects:
        * blobs: contents of files
        * trees: a list of blobs and trees, directory
        * commits: reference a tree and one or more parent commits
        * tags: refer to a particular commit by name
    + commit objects: `:Gedit <SHA code>`
        * similar `git show <SHA>`
        * `<Enter>` on a reference to a parent commit to show it
        * `<Enter>` on a reference to a tree to show it
        * `<Enter>` on a diff summary line to diff the specified file
            before and after the commit.
    + tree objects:
        * `a` to show more information of the tree
        * you can navigate the tree as in a file system, use `<Enter>`
            and `<C-o>` to go back and forth
    + `:Gbrowse` anywhere to open GitHub URL in a browser
- Status line: show branch in the status line
    + `set statusline+=%{FugitiveStatusline()}`

### Colorscheme

- https://github.com/morhetz/gruvbox
    + Terminal specific: https://github.com/morhetz/gruvbox/wiki/Terminal-specific
    + iterm2, tmux
    + https://web.archive.org/web/20190121063455/https://medium.com/@dubistkomisch/how-to-actually-get-italics-and-true-colour-to-work-in-iterm-tmux-vim-9ebe55ebc2be
- http://vimcolors.com/

### Language pack

- https://github.com/sheerun/vim-polyglot
    + List of useful plugins

### ultisnip

- https://github.com/SirVer/ultisnips
    + Snippets

### Motion

- https://github.com/easymotion/vim-easymotion
- https://github.com/justinmk/vim-sneak
- https://github.com/kshenoy/vim-signature

### Fuzzy Finder

- https://github.com/kien/ctrlp.vim
- https://github.com/junegunn/fzf.vim

### Status line

- https://github.com/itchyny/lightline.vim
- https://github.com/vim-airline/vim-airline

### Coding

- https://github.com/vim-syntastic/syntastic
- https://github.com/w0rp/ale
- Class outline: https://vimawesome.com/plugin/tagbar
- https://vimawesome.com/plugin/the-nerd-commenter
- https://vimawesome.com/plugin/commentary-vim
- https://vimawesome.com/plugin/youcompleteme

### Editing

- https://github.com/tpope/vim-surround
- https://github.com/terryma/vim-multiple-cursors
- https://github.com/Yggdroot/indentLine
- https://github.com/mattn/emmet-vim
- https://vimawesome.com/plugin/tabular


### Productivity

- https://vimawesome.com/plugin/vim-orgmode

### Misc

- Tags manager
    + https://github.com/ludovicchabant/vim-gutentags
- Search tools wrapper
    + https://github.com/mileszs/ack.vim
- Multiple cursors
    + https://github.com/terryma/vim-multiple-cursors
    + This can be achieve by vim using visual block mode and substitute
        operator.
- Range, pattern, and substitute preview
    + https://github.com/markonm/traces.vim
    + Preview the change before run it
- Automatically detect tab settings in a new codebase
    + https://github.com/tpope/vim-sleuth

## Key mapping

### Overview

- Learn more about mapping: `:h map.txt`
- Unmap a key: get the default behavior back
    + `:unmap <key_binding>`
- List all the mappings by plugins and users
    + `:map`
- All default mappings and commands: `:h index.txt`
- Nested and recursive use of mapping: `:map {lhs} {rhs}`
- Avoid nested and recursive mappings: `:noremap {lhs} {rhs}`
- Remove the mapping of {lhs}: `:unmap {lhs}`
- Remove ALL mappings (including the default mappings):
    + `:mapclear`

### Mapping and Modes

There are six sets of mappings
- For Normal mode: When typing commands.
- For Visual mode: When typing commands while the Visual area is
  highlighted.
- For Select mode: like Visual mode but typing text replaces the
  selection.
- For Operator-pending mode: When an operator is pending (after "d",
  "y", "c",
  etc.).
- For Insert mode.  These are also used in Replace mode.
- For Command-line mode: When entering a ":" or "/" command.

Special case: While typing a count for a command in Normal mode, mapping
zero is disabled.  This makes it possible to map zero without making it
impossible to type a count with a zero.

```help
Overview of which map command works in which mode.  More details below.

     COMMANDS                    MODES ~
:map   :noremap  :unmap     Normal, Visual, Select, Operator-pending
:nmap  :nnoremap :nunmap    Normal
:vmap  :vnoremap :vunmap    Visual and Select
:smap  :snoremap :sunmap    Select
:xmap  :xnoremap :xunmap    Visual
:omap  :onoremap :ounmap    Operator-pending
:map!  :noremap! :unmap!    Insert and Command-line
:imap  :inoremap :iunmap    Insert
:lmap  :lnoremap :lunmap    Insert, Command-line, Lang-Arg
:cmap  :cnoremap :cunmap    Command-line
:tmap  :tnoremap :tunmap    Terminal-Job


        COMMANDS                                       MODES ~
                                       Normal  Visual+Select  Operator-pending ~
:map   :noremap   :unmap   :mapclear     yes        yes        yes
:nmap  :nnoremap  :nunmap  :nmapclear    yes         -          -
:vmap  :vnoremap  :vunmap  :vmapclear     -         yes         -
:omap  :onoremap  :ounmap  :omapclear     -          -         yes
```

## Improve performance ##

- Syntax highlighting
    + Slow because of using regular expressions
    + Change regex engine: `:h regexpengine`

```vim
:syntax off                      " radical
:set synmaxcol=200               " arbitrary number < 3000 (default value)
:set foldmethod=manual           " anything other than 'syntax'
:set foldmethod=indent
:set noshowmatch                 " it's off by default but well
```

- Misusing auto commands
    + Remove unnecessary auto commands: `autocmd`
- Redrawing
    + Slow because of many things to redraw
    + `set lazyredraw`
- Debug for slow scrolling
    + https://eduncan911.com/software/fix-slow-scrolling-in-vim-and-neovim.html
    + `:syntime on` then scroll up and down a lot to record the info
    + After 10 second or so, `:syntime report`
    + It lists all the slow functions and regex patterns
- Debug for starting time
    + `vim --startuptime log`
- Built-in profiling support

```vim
"The profile.log is in your Vim session's current directory
:profile start profile.log
:profile func *
:profile file *
" At this point do slow actions
:profile pause
:noautocmd qall!
```


# vimdiff

- `[c`: previous change
- `]c`: next change
- `do`: diff obtain = diffget, get the change from the other buffer
    + This can work with the visual mode to select only a portion of a
        hunk.
- `dp`: diffput, put the change to the other buffer
    + This can work with the visual mode to select only a portion of a
        hunk.
- `:diffupdate`: update the diff highlighting and folds

# All Vim's lists

- Jump list: Vim records what it calls “jump” motions, motions that
    generally can take you to a distant location in your buffer or to a
    different buffer.
    + `:jumps`: show jump list
    + `<C-o>`: previous jump
    + `<C-i>`: next jump
- Change list: Each undoable edit you make in a buffer adds an entry to
    the change list, which records the cursor location. You can
    therefore jump through the locations of the changes you’ve made.
    + `:changes`: show change list
    + `g;`: older change
    + `g,`: newer change
- Quickfix list: The quickfix list, generally speaking, provides a way
    of storing and traversing a list of locations across files. The
    quickfix list can be populated from the output of compilers and
    linters via :make, from searches with :grep, and so on.
    + `:copen`: open quickfix list
    + `:cclose`: close quickfix list
    + `:cprevious`: previous location
    + `:cnext`: next location
    + `:cfirst`: first location
    + `:clast`: last location
- Buffer list: The buffer list maintains a listing of all the buffers in
    the current editing session, including those that are hidden.
    + `:buffers` show buffer list
    + `:bprevious` previous buffer
    + `:bnext` next buffer
    + `:bfirst` first buffer
    + `:blast` last buffer
- Argument list: The arglist is populated with the file paths specified
    on the command line when starting Vim, and can also be manipulated
    from within Vim with the :args family of commands. The arglist can
    be useful for collecting a bunch of files to act on, such as
    performing a search and replace.
    + `:args` show argument list
    + `:previous` previous file
    + `:next` next file
    + `:first` first file
    + `:last` last file
- Tag stack: Vim remembers each tag you jump to, for example by invoking
    <C-]>, and the location from which you jumped by pushing an entry
    onto the tag stack. By popping an entry from the stack, you are
    returned to your previous location.
    + `:tags` show tag stack
    + `:pop` previous tag
    + `:tag` next tag
- Tag match list: Every time you jump to a tag, it gets pushed onto the
    tag stack (see above). When there are multiple matches for a tag,
    however, they can be navigated through the tag match list.
    + `:tselect` show tag match list
    + `:tprevious` previous tag
    + `:tnext` next tag
    + `:tfirst` first tag
    + `:tlast` last tag

# Spell checking

- Enable global spell checking: `set spell`
- `]s` find the next misspelled word
- `[s` find the previous misspelled word
- `]S` similar `]s` but only stop at bad words instead of rare words or
    words for another region.
- `[S`
- `z=` suggestions for that particular words.
- `set spell spelllang=en_us` set spell language.
- `zg` add word into the dictionary.
- `zw` mark the word as a wrong (bad) word, if the word already appears
    in spellfile it is turned into a comment line.
    + clean up the spellfile by running `:runtime spell/cleanadd.vim`
    + Deletes all comment lines, except the ones that start with "##".
        Use "##" to add comment that you want to keep.
- `zug` and `zuw` undo `zg` and `zw`
- Spell check by file type
    + `autocmd FileType gitcommit,latex,tex,md setlocal spell`

# Cscope

Cscope is a tool like ctags, but think of it as ctags on steroids since
it does a lot more than what ctags provides.  In Vim, jumping to a
result from a cscope query is just like jumping to any tag; it is saved
on the tag stack so that with the right keyboard mappings, you can jump
back and forth between functions as you normally would with |tags|.

- `:h cscope`

# Troubleshooting

## Error: * not found *

- Check runtime path: `:set runtimepath?`

# Editor Wars

```txt
Take away of a programmer

I’m done making excuses for why I use Emacs/Vim over PyCharms. I might
be able to edit that line 5 times faster in Vim that I can in PyCharms,
but if my experience with Emacs taught me anything, it’s that the editor
doesn’t matter as much as we’d like to believe.

As programmers, we’re told to use the right tool for the job. I have
finally realised that Vim/Emacs aren’t the right tools for
Python/Django. For me at least. For Golang, I haven’t found anything
better than Vim. For general notes and to-dos, Emacs with Org Mode is
the best. Magit is the best Git frontend I’ve seen. I prefer using it
over the Git CLI. For editing files that are GBs in size, Vim blows
everything else out of the water. For Clojure (which I got interested in
because of Emacs LISP) Emacs is straight down the only thing I’ll
consider using. And I’m sure that for other statically typed languages
like Rust, C, C++, Emacs and Vim are crazy awesome, and I’ll probably
use them over anything else. But for Python, PyCharms is the best I’ve
seen. And I’m going to give it a try now.

I guess this is just a rant, something I had to get off my chest for a
long while. I’ve had arguments with many people over why Vim beats their
editor of choice. This is my way of accepting that they were probably
smarted than me in their choices.

This is my way of accepting that I don’t need to use Vim/Emacs to be
good at my job. That it’s OK to not follow the culture when you can’t
seem to fit in. And this is my effort to help the next 15 year old who
searches for “Vim vs Emacs”. Don’t worry about it. Use whatever feels
natural, and works best for the environment you’re working in.

I will keep using Vim on the remote machines I manage and for Golang. I
will keep using Emacs for Org Mode. And from now on, I’ll use PyCharms
for Python.

One of the surprising discoveries during this journey for me was just
how limited I believed my abilities to adapt were. I had convinced
myself that I could never move to another editor. But after using Vim
for more than 7 years, moving to Emacs successfully over a period of
less than 2 months opened up my eyes.
```

# References

[1]: http://vimcasts.org/episodes/the-file-explorer/ "Vimcasts - 15. The file explorer"
[2]: http://vim.wikia.com/wiki/Learn_to_use_help "Learn how to use help"
[plugins]: https://vimawesome.com/
