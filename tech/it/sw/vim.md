# [Overview][wiki]

Vim (a contraction of Vi IMproved) is a clone of Bill Joy's vi text
editor program for Unix. It was written by Bram Moolenaar based on
source for a port of the Stevie editor to the Amiga.

Initial release in November 1991.

Cheatsheet
- https://quickref.me/vim
- https://dev.to/iggredible/the-only-vim-insert-mode-cheatsheet-you-ever-needed-nk9
- https://learnbyexample.github.io/vim_reference/Insert-mode.html

# Help

- If you encounter the error: `E:149 no help for help.txt`, you need to
  regenerate help tags file: `:helptags ALL`
- `:help` help facility built-in
- `:h help` how to use help
- `:h` help system
- `vimtutor` : basic commands tutorials
- `:h key-notation`: these names for keys are used in the documentation.

## Learn to use help

- `:h <patt>` the Tab to scroll through topics that start with <patt>
- `<C-]>` to follow the link
- `<C-o>`: previous location, `<C-i>`: next location
- `:helpgrep \csearch.\{,12}file`
    + `\c` case insensitive
    + the pattern finds `search` then up to 12 characters followed by
      `file`
    + the results are loaded into quickfix list.
    + `:clist` to see all the quickfix list

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
    + Vim has a number of internal variables and switches which can be
      set to achieve special effects.  These options come in three
      forms: boolean, number, string
    + `:h options`

```vim
" Create file ~/.vim/ftplugin/help.vim
nnoremap <buffer> <CR> <C-]>
nnoremap <buffer> <BS> <C-T>
nnoremap <buffer> o /'\l\{2,\}'<CR>
nnoremap <buffer> O ?'\l\{2,\}'<CR>
nnoremap <buffer> s /\|\zs\S\+\ze\|<CR>
nnoremap <buffer> S ?\|\zs\S\+\ze\|<CR>
```



# Features and improvements over vi

## Customization

Part of Vim's power is that it can be extensively customized.
- Change basic interface
- Define personalized key mappings
- Abbreviations to automate sequences of keystrokes
- Call internal or user defined functions

Plugins available that will extend or add new functionality to Vim.
- Vim's internal scripting language - vimscript (viml)
- Lua, Perl, Python, Racket, Ruby, and Tcl

## Search and replace

- Search
    + `/`: forward (can use arrow to select previous search patterns)
    + `?`: backward (can use arrow to select previous search patterns)
    + `q/`: view the search buffer that contains all previous search
      patterns.
- Change each "foo" to "bar" in the current line: `:s/foo/bar/g` and
  have confirm : `:s/foo/bar/gc`
- Change each "foo" to "bar" in all the lines: `:%s/foo/bar/g` and have
  confirm: `:%s/foo/bar/gc`
- Change each "foo" to "bar" for all lines from line 5 to line 12:
  `:5,12s/foo/bar/gc`
- **USEFUL**
    + `:%s/EG[ ,A-Z]*\ze\s/\0, ZA/g`
        * Find all string start with `EG`, end with space (`\ze\s`)
        * `\0`: all the match, appends with `, ZA`
    + Vim lookahead and lookbehind regex
        * https://vim.fandom.com/wiki/Regex_lookahead_and_lookbehind
        * https://stackoverflow.com/questions/18391665/vim-positive-lookahead-regex
        * `:h \@=`, `:h \zs`, `:h \ze`
    + Back references to matched patterns
        * `:h \0`
        * https://vim.fandom.com/wiki/Search_and_replace#Details

## Copy and paste

- Copy to clipboard and paste from clipboard (this is much faster than
  using C+v to paste from outside clipboard to vim)
    + Using registers
        * X11's primary register: `"*y`, `"*p`
        * X11's clipboard register: `"+y`, `"+p`
    + Disable `CMD/CTRL + v` on terminal or operating system or at Vim
      configuration to prevent accidentally using normal pasting.
- Configuration at `.vimrc` : `xnoremap p pgvy` it mean *p* will replay
  with *pgvy*, *p* to paste and *go* to re-select what was originally
  selected, *y* to copy it again.
- Paste multiple copy: *<number>p* e.g: *30p* to paste 30 time of copy
  text.

## Others

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


# Resources

## Links

- [Vim ways](https://vimways.org)
- [Thoughtbot blog](https://thoughtbot.com/blog/tags/vim)
- The Patient Dimmer: http://romainl.github.io/the-patient-vimmer/
- [Recommendations](https://www.vi-improved.org/recommendations/)
- [Thoughtbot Tutorials](https://upcase.com/vim)
- [vimcast](http://vimcasts.org/)
- [vim-gusts](https://gist.github.com/romainl/4b9f139d2a8694612b924322de1025ce)
    + [idiomatic-vimrc](https://github.com/romainl/idiomatic-vimrc)
    + [built-in](https://gist.github.com/romainl/047aca21e338df7ccf771f96858edb86)
    + [macros](https://gist.github.com/romainl/9721c7dd13c30714f568063e03c106dd)
- Some examples for .vimrc to learn more tricks
    + https://stackoverflow.com/questions/164847/what-is-in-your-vimrc
- Some external programs to use with Vim
    + https://www.reddit.com/r/vim/comments/7bj837/favorite_console_tools_to_use_with_vim/:

## Books

- [Books](http://iccf-holland.org/click5.html)
- Practical Vim - 2nd edition
- [Modern Vim](https://pragprog.com/book/modvim/modern-vim)
- Learn Vimscript the Hard Way
    + http://learnvimscriptthehardway.stevelosh.com/


# 7 habits of effective text editing (Bram Moolenaar)

## Move around quickly

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
- `tpope/vim-rsi`: deadline Emacs' mappings
    + `<C-e>`: to the end of the line
    + `<C-f>`: forward one character

## Don't type it twice

- `:s`: substitute
- `*`: find word and `cw`
    + `n` go to next item in the search results
- `.`: repeat the change
    + `m <mark>`: mark the location to come back later in normal mode
        * e.g., `ma`, `mb`, ...
        * go to the mark at the beginning of the line: `'<mark>`
            - e.g., `'a`, `'b`, ...
        * go to the exact location of the mark: <backtick><mark>
            - where <backtick> is the symbol on the keyboard
            - e.g., <backtick>a, ...
- `<C-n>`: auto complete in insert mode
- `qa` start recording a macro into register `a` (total 26 registers)
    + hit `q` again to stop recording
    + apply the macro by typing `@a`
    + should use commands to move over text objects (words, sentences,
        etc.) instead of characters
- Snippets

## Fix it when it's wrong

- Correct mistakes using spell check
    + `:setlocal spell spelllang=en_us`
    + `:h spell`

```vim
" A mapping to quickly correct the previous spelling error
" <C-g>u: insert an undo break
" <Esc>[s: go to the previous spelling error
" 1z=: replace the error by the first suggestion
" `]: move to the last insert position
" a: enter insert mode at append position
" <C-g>u: insert another undo break
inoremap <C-l> <C-g>u<Esc>[s1z=`]a<C-g>u
```

## Work with multiple files

- Using a fuzzy finder to quickly find files and search the file content
- `[I`: show a list of matched for the function name under the cursor in
    included files.
- Using preview-tag mechanism, an open special preview window.

## Text is structured

- edit-compile-fix cycle `:make` command
    + which starts your compilation, catches the errors it produces and
      lets you jump to the error locations to fix the problems

# Basic Usage

## Undo - Redo in normal mode

- `u`: undo
- `Ctrl + r`: redo

## Folding

- https://vim.fandom.com/wiki/Folding

### Creating and deleting folds

- Only works for `foldmethod` is `manual` or `marker`
- `zf{motion}`: manually create a fold in the range of motion
    + `zf'a`: fold from the current line to there the mark `a` has been
      set
    + `zf3j`: fold the current line along with the following 3 lines
    + You can enter `Visual` mode then select the lines, and hit `zf` to
      fold
- `zd`: delete the fold at the cursor

### Opening and closing folds

- `zc`: close a fold
    + When count is given, that many folds deep will be closed.
    + In visual mode one level of folds is closed for all lines in the
      selected area.
- `zo`: open a fold
- `za`: toggle open and close a fold
- `zC`, `zO`, `zA`: operate on all folding levels (i.e., close all folds
  at the cursor)

- `zx`: undo manually opened and closed folds, re-apply `foldlevel`,
  then do `zv`
- `zX`: undo manually opened and closed folds, re-apply `foldlevel`
- `zr`: reduces folding by opening one more level of folds throughout
  the whole buffer (the cursor position is not relevant)
- `zR`: open all folds
- `zm`: gives more folding by closing one more level of folds throughout
  the whole buffer
- `zM`: close all folds
- `zn`: fold none: reset `foldenable`. All folds will be open.
- `zN`: fold normal: set `foldenable`. All folds will be as they were
  before

### Moving over folds

- `[z`: move to the start of the current open fold.
- `]z`: move to the end of the current open fold.
- `zj`: move downwards to the start of the next fold.
- `zk`: move upwards to the end of the previous fold.

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
    + Alternate file: the last edited file in the current window.
        * https://stackoverflow.com/q/5182852/1683888
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

- CHECK `.vimrc` first to check for personal shortcuts before using
  built-in shortcuts

`:h window-resize`

| Keystrokes  | Buffer Contents                          |
|-------------|------------------------------------------|
| `<C-w>=`    | Equalize width and height of all windows |
| `<C-w>_`    | Maximize height of the active window     |
| `[N]<C-w>_` | Set active window height to [N] rows     |
| `<C-w>-`    | Decrease active window's height 2 points |
| `<C-w>+`    | Increase active window's height 2 points |
| `<C-w> >`   | Increase active window's width 2 points  |
| `<C-w> <`   | Decrease active window's width 2 points  |

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

## `myvim` - A script to a portable bundle of my Vim environment

- https://github.com/junegunn/myvim
    + https://github.com/junegunn/myvim/blob/master/myvim
- This can be used to create a executable file to run on any servers to
  have the exact same Vim environment as your personal Vim environment.
- `myvim` creates a tar archive of your .vimrc and .vim directory and
  append it to a small bash script that starts Vim with your usual
  settings and plugins.

## Search for visually selected text

- https://vim.fandom.com/wiki/Search_for_visually_selected_text
- A Vim script in `.vim/plugin/vsearch.vim`

## Open a clean/fresh vim session that does not take any custom configurations

- `vim --clean [file]`
- https://vi.stackexchange.com/questions/6112/how-can-i-get-vim-to-ignore-all-user-configuration-as-if-it-were-freshly-instal

## Math: simple calculations

- Use expression register
    + `<C-r>=7*7<CR>`
- Increment and decrement shortcuts
    + `<C-a>` and `C-x`
- External tools
    + `bc`, `calc`


## Redir - redirect the output of a Vim or external command into a scratch buffer

- https://gist.github.com/romainl/eae0a260ab9c135390c30cd370c20cd7
- `autoload/redir.vim`

## Paste yanked text into the Vim command line

- https://stackoverflow.com/questions/3997078/how-to-paste-yanked-text-into-the-vim-command-line/3997110#3997110
- https://stackoverflow.com/questions/4268532/how-to-execute-selected-text-as-vim-commands

## Text Objects

- https://blog.carbonfive.com/vim-text-objects-the-definitive-guide/

## Working with JSON

- `:%`: the entire range of the file
- Reformat
    + `:%!jq` or `:%!jq .`: this does not give us a compacted JSON
    + `:%!underscore print`
- Underscore CLI: https://github.com/ddopson/underscore-cli

## Spawn a new shell in a Vim window

- `:term[inal]`
- `:terminal` vs `:shell`
    + https://vi.stackexchange.com/questions/27736/in-vim8-2-is-there-any-difference-between-using-term-vs-shell

## Spawn a new shell in your terminal (not in a Vim window)

- The only way to back in Vim is to terminate the shell.

## Autoload changes to a file to your current buffer

- https://unix.stackexchange.com/questions/149209/refresh-changed-content-of-file-opened-in-vim/383044#383044

```
" Triger `autoread` when files changes on disk
" https://unix.stackexchange.com/questions/149209/refresh-changed-content-of-file-opened-in-vim/383044#383044
" https://vi.stackexchange.com/questions/13692/prevent-focusgained-autocmd-running-in-command-line-editing-mode
    autocmd FocusGained,BufEnter,CursorHold,CursorHoldI *
            \ if mode() !~ '\v(c|r.?|!|t)' && getcmdwintype() == '' | checktime | endif

" Notification after file change
" https://vi.stackexchange.com/questions/13091/autocmd-event-for-autoread
autocmd FileChangedShellPost *
  \ echohl WarningMsg | echo "File changed on disk. Buffer reloaded." | echohl None
```

## Vim as Java IDE

- SpaceVim
    + https://spacevim.org/use-vim-as-a-java-ide/
- https://jqno.nl/post/2020/09/09/my-vim-setup/

## Set filetype for a file

- `:set ft=markdown`

## Camel case motion

- Using `f/F/t/T<char>` to move to the next upper `<char>`
- Using `;` to repeat the motion in forward direction
- Using `,` to repeat the motion in backward direction

## Setting python version for Vim

```
" Set Python 3 as default Python for Vim
set pythonthreehome=/usr/local/Frameworks/Python.framework/Versions/3.7
set pythonthreedll=/usr/local/Frameworks/Python.framework/Versions/3.7/Python

```

## Close all buffers

- `:%bd` or `:%bd!`
- Close all buffers but this one: `:%bd|e#`

```vim
" Close all buffers except the current buffer
nnoremap <Leader>w :%bd <bar> e#<CR>

" Close all buffers
nnoremap <Leader>W :%bd<CR>
```

## Logging every autocommands events in a log file

- Create a `log-autocmds.vim` in `~/.vim/autoload/`

```vim
command! LogAutocmds call s:log_autocmds_toggle()

function! s:log_autocmds_toggle()
  augroup LogAutocmd
    autocmd!
  augroup END

  let l:date = strftime('%F', localtime())
  let s:activate = get(s:, 'activate', 0) ? 0 : 1
  if !s:activate
    call s:log('Stopped autocmd log (' . l:date . ')')
    return
  endif

  call s:log('Started autocmd log (' . l:date . ')')
  augroup LogAutocmd
    for l:au in s:aulist
      silent execute 'autocmd' l:au '* call s:log(''' . l:au . ''')'
    endfor
  augroup END
endfunction

function! s:log(message)
  silent execute '!echo "'
        \ . strftime('%T', localtime()) . ' - ' . a:message . '"'
        \ '>> /tmp/vim_log_autocommands'
endfunction

" These are deliberately left out due to side effects
" - SourceCmd
" - FileAppendCmd
" - FileWriteCmd
" - BufWriteCmd
" - FileReadCmd
" - BufReadCmd
" - FuncUndefined

let s:aulist = [
      \ 'BufNewFile',
      \ 'BufReadPre',
      \ 'BufRead',
      \ 'BufReadPost',
      \ 'FileReadPre',
      \ 'FileReadPost',
      \ 'FilterReadPre',
      \ 'FilterReadPost',
      \ 'StdinReadPre',
      \ 'StdinReadPost',
      \ 'BufWrite',
      \ 'BufWritePre',
      \ 'BufWritePost',
      \ 'FileWritePre',
      \ 'FileWritePost',
      \ 'FileAppendPre',
      \ 'FileAppendPost',
      \ 'FilterWritePre',
      \ 'FilterWritePost',
      \ 'BufAdd',
      \ 'BufCreate',
      \ 'BufDelete',
      \ 'BufWipeout',
      \ 'BufFilePre',
      \ 'BufFilePost',
      \ 'BufEnter',
      \ 'BufLeave',
      \ 'BufWinEnter',
      \ 'BufWinLeave',
      \ 'BufUnload',
      \ 'BufHidden',
      \ 'BufNew',
      \ 'SwapExists',
      \ 'FileType',
      \ 'Syntax',
      \ 'EncodingChanged',
      \ 'TermChanged',
      \ 'VimEnter',
      \ 'GUIEnter',
      \ 'GUIFailed',
      \ 'TermResponse',
      \ 'QuitPre',
      \ 'VimLeavePre',
      \ 'VimLeave',
      \ 'FileChangedShell',
      \ 'FileChangedShellPost',
      \ 'FileChangedRO',
      \ 'ShellCmdPost',
      \ 'ShellFilterPost',
      \ 'CmdUndefined',
      \ 'SpellFileMissing',
      \ 'SourcePre',
      \ 'VimResized',
      \ 'FocusGained',
      \ 'FocusLost',
      \ 'CursorHold',
      \ 'CursorHoldI',
      \ 'CursorMoved',
      \ 'CursorMovedI',
      \ 'WinEnter',
      \ 'WinLeave',
      \ 'TabEnter',
      \ 'TabLeave',
      \ 'CmdwinEnter',
      \ 'CmdwinLeave',
      \ 'InsertEnter',
      \ 'InsertChange',
      \ 'InsertLeave',
      \ 'InsertCharPre',
      \ 'TextChanged',
      \ 'TextChangedI',
      \ 'ColorScheme',
      \ 'RemoteReply',
      \ 'QuickFixCmdPre',
      \ 'QuickFixCmdPost',
      \ 'SessionLoadPost',
      \ 'MenuPopup',
      \ 'CompleteDone',
      \ 'User',
      \ ]
```


```vim
augroup EventLogging
  autocmd!
  autocmd BufNewFile * call s:Log('BufNewFile')
  autocmd BufReadPre * call s:Log('BufReadPre')
  autocmd BufRead * call s:Log('BufRead')
  autocmd BufReadPost * call s:Log('BufReadPost')
  autocmd BufReadCmd * call s:Log('BufReadCmd')
  autocmd FileReadPre * call s:Log('FileReadPre')
  autocmd FileReadPost * call s:Log('FileReadPost')
  autocmd FileReadCmd * call s:Log('FileReadCmd')
  autocmd FilterReadPre * call s:Log('FilterReadPre')
  autocmd FilterReadPost * call s:Log('FilterReadPost')
  autocmd StdinReadPre * call s:Log('StdinReadPre')
  autocmd StdinReadPost * call s:Log('StdinReadPost')
  autocmd BufWrite * call s:Log('BufWrite')
  autocmd BufWritePre * call s:Log('BufWritePre')
  autocmd BufWritePost * call s:Log('BufWritePost')
  autocmd BufWriteCmd * call s:Log('BufWriteCmd')
  autocmd FileWritePre * call s:Log('FileWritePre')
  autocmd FileWritePost * call s:Log('FileWritePost')
  autocmd FileWriteCmd * call s:Log('FileWriteCmd')
  autocmd FileAppendPre * call s:Log('FileAppendPre')
  autocmd FileAppendPost * call s:Log('FileAppendPost')
  autocmd FileAppendCmd * call s:Log('FileAppendCmd')
  autocmd FilterWritePre * call s:Log('FilterWritePre')
  autocmd FilterWritePost * call s:Log('FilterWritePost')
  autocmd BufAdd * call s:Log('BufAdd')
  autocmd BufCreate * call s:Log('BufCreate')
  autocmd BufDelete * call s:Log('BufDelete')
  autocmd BufWipeout * call s:Log('BufWipeout')
  autocmd BufFilePre * call s:Log('BufFilePre')
  autocmd BufFilePost * call s:Log('BufFilePost')
  autocmd BufEnter * call s:Log('BufEnter')
  autocmd BufLeave * call s:Log('BufLeave')
  autocmd BufWinEnter * call s:Log('BufWinEnter')
  autocmd BufWinLeave * call s:Log('BufWinLeave')
  autocmd BufUnload * call s:Log('BufUnload')
  autocmd BufHidden * call s:Log('BufHidden')
  autocmd BufNew * call s:Log('BufNew')
  autocmd SwapExists * call s:Log('SwapExists')
  autocmd FileType * call s:Log('FileType')
  autocmd Syntax * call s:Log('Syntax')
  autocmd EncodingChanged * call s:Log('EncodingChanged')
  autocmd TermChanged * call s:Log('TermChanged')
  autocmd VimEnter * call s:Log('VimEnter')
  autocmd GUIEnter * call s:Log('GUIEnter')
  autocmd GUIFailed * call s:Log('GUIFailed')
  autocmd TermResponse * call s:Log('TermResponse')
  autocmd QuitPre * call s:Log('QuitPre')
  autocmd VimLeavePre * call s:Log('VimLeavePre')
  autocmd VimLeave * call s:Log('VimLeave')
  autocmd FileChangedShell * call s:Log('FileChangedShell')
  autocmd FileChangedShellPost * call s:Log('FileChangedShellPost')
  autocmd FileChangedRO * call s:Log('FileChangedRO')
  autocmd ShellCmdPost * call s:Log('ShellCmdPost')
  autocmd ShellFilterPost * call s:Log('ShellFilterPost')
  autocmd FuncUndefined * call s:Log('FuncUndefined')
  autocmd SpellFileMissing * call s:Log('SpellFileMissing')
  autocmd SourcePre * call s:Log('SourcePre')
  autocmd SourceCmd * call s:Log('SourceCmd')
  autocmd VimResized * call s:Log('VimResized')
  autocmd FocusGained * call s:Log('FocusGained')
  autocmd FocusLost * call s:Log('FocusLost')
  autocmd CursorHold * call s:Log('CursorHold')
  autocmd CursorHoldI * call s:Log('CursorHoldI')
  autocmd CursorMoved * call s:Log('CursorMoved')
  autocmd CursorMovedI * call s:Log('CursorMovedI')
  autocmd WinEnter * call s:Log('WinEnter')
  autocmd WinLeave * call s:Log('WinLeave')
  autocmd TabEnter * call s:Log('TabEnter')
  autocmd TabLeave * call s:Log('TabLeave')
  autocmd CmdwinEnter * call s:Log('CmdwinEnter')
  autocmd CmdwinLeave * call s:Log('CmdwinLeave')
  autocmd InsertEnter * call s:Log('InsertEnter')
  autocmd InsertChange * call s:Log('InsertChange')
  autocmd InsertLeave * call s:Log('InsertLeave')
  autocmd InsertCharPre * call s:Log('InsertCharPre')
  autocmd TextChanged * call s:Log('TextChanged')
  autocmd TextChangedI * call s:Log('TextChangedI')
  autocmd ColorScheme * call s:Log('ColorScheme')
  autocmd RemoteReply * call s:Log('RemoteReply')
  autocmd QuickFixCmdPre * call s:Log('QuickFixCmdPre')
  autocmd QuickFixCmdPost * call s:Log('QuickFixCmdPost')
  autocmd SessionLoadPost * call s:Log('SessionLoadPost')
  autocmd MenuPopup * call s:Log('MenuPopup')
  autocmd CompleteDone * call s:Log('CompleteDone')
  autocmd User * call s:Log('User')
augroup END

function! s:Log(eventName) abort
  silent execute '!echo '.a:eventName.' >> log'
endfunction
```


## Creating folders / directories on save

```vim
" Put this function in the .vim/autoload/vimrc.vim
function s:MkNonExDir(file, buf)
    if empty(getbufvar(a:buf, '&buftype')) && a:file!~#'\v^\w+\:\/'
        let dir=fnamemodify(a:file, ':h')
        if !isdirectory(dir)
            call mkdir(dir, 'p')
        endif
    endif
endfunction

" Add this autocmd to the augroup in .vimrc file
augroup BWCCreateDir
    autocmd!
    autocmd BufWritePre * :call s:MkNonExDir(expand('<afile>'), +expand('<abuf>'))
augroup END
```

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

## SpaceVim

- https://spacevim.org/
- https://spacevim.org/use-vim-as-ide/

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

## Plug-in manager

- Discusses:
    + http://vi.stackexchange.com/questions/388/what-is-the-difference-between-the-vim-package-managers
    + https://www.reddit.com/r/vim/comments/36ak7j/do_you_use_a_vim_plugin_manager_if_so_which_one/
    + https://www.reddit.com/r/vim/comments/1w4udb/best_vim_plugin_manager/
- [Vim-plug](https://github.com/junegunn/vim-plug)
    + Install a plugin: add a plug line in vimrc, then source the vimrc,
      then run `PlugInstall`
    + Remove a plugin: remove the plug line in vimrc, then source the
      vimrc, then run `PlugClean`
- [pathogen](https://github.com/tpope/vim-pathogen/)
- [Vundle](https://github.com/VundleVim/Vundle.vim)
- [NeoVundle](https://github.com/Shougo/neobundle.vim)

## Autoloading

- https://learnvimscriptthehardway.stevelosh.com/chapters/53.html
- Making custom plugins more efficient.
- Autoload lets you delay loading code until it's actually
  needed. You'll take a slight performance hit overall, but if your
  users don't always use every single bit of code in your plugin
  autoloading can be a huge speedup.
- To reload a Vim script:
    + `:runtime autload/foobar.vim`
    + `:source <absolute-path-to-foobar.vim>`
    + Close Vim and re-open!!!

## Plugins

- `:h plugin`
    + Global plugin: `.vim/plugin`
    + File type plugin: `.vim/ftplugin`

### Misc

- coc.nvim
    + https://github.com/neoclide/coc.nvim
    + Language Server Protocol client
    + Features
        * Code completion (main)
- Showing marks
    + vim-signature: https://github.com/kshenoy/vim-signature
    + vim-markbar: https://github.com/Yilin-Yang/vim-markbar
    + Clear all marks: https://stackoverflow.com/questions/11450817/vim-how-do-i-clear-all-marks
        * `:delmarks!`: all marks excepts A-Z and 0-9
        * `:delmarks A-Z0-9`: delete marks A-Z and 0-9


- Neomake (similar ale): https://github.com/neomake/neomake
- Python-mode: https://github.com/python-mode/python-mode
- Debugging
    + https://github.com/idanarye/vim-vebugger
    + https://github.com/vim-vdebug/vdebug
    + https://github.com/gilligan/vim-lldb
- Undotree: https://github.com/mbbill/undotree
- Mappings for tags:
    + https://github.com/tpope/vim-ragtag
- Tags manager
    + https://github.com/ludovicchabant/vim-gutentags
- Search tools wrapper
    + https://github.com/mileszs/ack.vim
- Multiple cursors
    + https://github.com/terryma/vim-multiple-cursors
    + This can be achieve by vim using visual block mode and substitute
        operator.
- Automatically detect tab settings in a new codebase
    + https://github.com/tpope/vim-sleuth


### vim-dadbod-ui

- https://github.com/kristijanhusak/vim-dadbod-ui
    + Auto complete: https://github.com/kristijanhusak/vim-dadbod-completion
        * Key mapping: `<C-Space>` or Omnifunc `<C-x><C-o>`
- A Vim plugin to connect to databases (PostgresSQL, RDS, etc.)
- `:DBUI`: open the UI drawer on the left side
    + `?` to open help
- Also need to install database CLI for each database that we want to
  connect to, for example `psql` for PostGreSQL.
- URL for PostGresQSQL
    + `postgresql://[user[:password]@][netloc][:port][/dbname][?extra=value[&other=other-value]]`
    + `postgresql://booker:testpw@ips-na-prod1.cluster-link.us-east-1.rds.amazonaws.com:8200/ips1na`
    + `postgresql://booker:amazon#789@ips-eu-prod1.cluster-cuqbnimdgye6.eu-west-1.rds.amazonaws.com:8200/ips1eu`

### vim-easymotion

- vim-easymotion: https://github.com/easymotion/vim-easymotion
    + `:h easymotion` for manual

### vimtex

#### Intro

- It needs a Vim server for call functionality and backward search from
  PDF viewer to Vim.
    + To run a Vim server, Vim have to be compiled with `+clientserver`.
    + On macOS use MacVim instead of console vim to have this feature.
- Default mappings

#### Default mappings

```help
---------------------------------------------------------------------~
LHS              RHS                                          MODE~
---------------------------------------------------------------------~
<localleader>li  |<plug>(vimtex-info)|                           `n`
<localleader>lI  |<plug>(vimtex-info-full)|                      `n`
<localleader>lt  |<plug>(vimtex-toc-open)|                       `n`
<localleader>lT  |<plug>(vimtex-toc-toggle)|                     `n`
<localleader>lq  |<plug>(vimtex-log)|                            `n`
<localleader>lv  |<plug>(vimtex-view)|                           `n`
<localleader>lr  |<plug>(vimtex-reverse-search)|                 `n`
<localleader>ll  |<plug>(vimtex-compile)|                        `n`
<localleader>lL  |<plug>(vimtex-compile-selected)|               `nx`
<localleader>lk  |<plug>(vimtex-stop)|                           `n`
<localleader>lK  |<plug>(vimtex-stop-all)|                       `n`
<localleader>le  |<plug>(vimtex-errors)|                         `n`
<localleader>lo  |<plug>(vimtex-compile-output)|                 `n`
<localleader>lg  |<plug>(vimtex-status)|                         `n`
<localleader>lG  |<plug>(vimtex-status-all)|                     `n`
<localleader>lc  |<plug>(vimtex-clean)|                          `n`
<localleader>lC  |<plug>(vimtex-clean-full)|                     `n`
<localleader>lm  |<plug>(vimtex-imaps-list)|                     `n`
<localleader>lx  |<plug>(vimtex-reload)|                         `n`
<localleader>lX  |<plug>(vimtex-reload-state)|                   `n`
<localleader>ls  |<plug>(vimtex-toggle-main)|                    `n`
dse              |<plug>(vimtex-env-delete)|                     `n`
dsc              |<plug>(vimtex-cmd-delete)|                     `n`
ds$              |<plug>(vimtex-env-delete-math)|                `n`
dsd              |<plug>(vimtex-delim-delete)|                   `n`
cse              |<plug>(vimtex-env-change)|                     `n`
csc              |<plug>(vimtex-cmd-change)|                     `n`
cs$              |<plug>(vimtex-env-change-math)|                `n`
csd              |<plug>(vimtex-delim-change-math)|              `n`
tsc              |<plug>(vimtex-cmd-toggle-star)|                `n`
tse              |<plug>(vimtex-env-toggle-star)|                `n`
tsd              |<plug>(vimtex-delim-toggle-modifier)|          `nx`
tsD              |<plug>(vimtex-delim-toggle-modifier-reverse)|  `nx`
<F7>             |<plug>(vimtex-cmd-create)|                     `nxi`
]]               |<plug>(vimtex-delim-close)|                    `i`
ac               |<plug>(vimtex-ac)|                             `xo`
ic               |<plug>(vimtex-ic)|                             `xo`
ad               |<plug>(vimtex-ad)|                             `xo`
id               |<plug>(vimtex-id)|                             `xo`
ae               |<plug>(vimtex-ae)|                             `xo`
ie               |<plug>(vimtex-ie)|                             `xo`
a$               |<plug>(vimtex-a$)|                             `xo`
i$               |<plug>(vimtex-i$)|                             `xo`
aP               |<plug>(vimtex-aP)|                             `xo`
iP               |<plug>(vimtex-iP)|                             `xo`
%                |<plug>(vimtex-%)|                              `nxo`
]]               |<plug>(vimtex-]])|                             `nxo`
][               |<plug>(vimtex-][)|                             `nxo`
[]               |<plug>(vimtex-[])|                             `nxo`
[[               |<plug>(vimtex-[[)|                             `nxo`
]m               |<plug>(vimtex-]m)|                             `nxo`
]M               |<plug>(vimtex-]M)|                             `nxo`
[m               |<plug>(vimtex-[m)|                             `nxo`
[M               |<plug>(vimtex-[M)|                             `nxo`
]/               |<plug>(vimtex-]/|                              `nxo`
]*               |<plug>(vimtex-]star|                           `nxo`
[/               |<plug>(vimtex-[/|                              `nxo`
[*               |<plug>(vimtex-[star|                           `nxo`
K                |<plug>(vimtex-doc-package)|                    `n`
---------------------------------------------------------------------~
```


### goyo.vim and limelight.vim

- Distraction-free mode in Vim.
- `<Leader>d`
- https://github.com/junegunn/goyo.vim

### traces.vim

- Range, pattern, and substitute preview
    + https://github.com/markonm/traces.vim
    + Preview the change before run it

### vim-commentary

- `gc{motion}` Comment or uncomment lines that {motion} moves over.
- `gcc` Comment or uncomment [count] lines.
- `{Visual}gc` Comment or uncomment the highlighted lines.
- `gc` Text object for a comment (operator pending mode
              only.)
- `gcgc` or `gcu` Uncomment the current and adjacent commented lines.
- `:[range]Commentary` Comment or uncomment [range] lines

### gv.vim

- Git browser

#### Commands

- `:GV` to open commit browser
    - You can pass `git log` options to the command, e.g. `:GV -S foobar`.
- `:GV!` will only list commits that affected the current file
- `:GV?` fills the location list with the revisions of the current file

`:GV` or `:GV?` can be used in visual mode to track the changes in the
selected lines.

#### Mappings

- `o` or `<cr>` on a commit to display the content of it
- `o` or `<cr>` on commits to display the diff in the range
- `O` opens a new tab instead
- `gb` for `:Gbrowse`
- `]]` and `[[` to move between commits
- `.` to start command-line with `:Git [CURSOR] SHA` à la fugitive
- `q` to close


### vim-rhubarb

- Use :Gbrowse to browse GitHub URL.

### ale

- Configure ALE with CoC
    + https://github.com/dense-analysis/ale#faq-coc-nvim

- `:h ale`

```vim
"""" ale configuration

let g:ale_enabled = 0   " Disable ALE at beginning

"""" ale mapping

nmap <Leader>at <Plug>(ale_toggle)
nmap <Leader>aT <Plug>(ale_toggle_buffer)
```

#### markdown-preview.nvim

```vim
"""" markdown-preview.nvim mapping

nmap <Leader>mp <Plug>MarkdownPreview
nmap <Leader>ms <Plug>MarkdownPreviewStop
```


### vim-obsession

- `:Obsession {file}` invoke :mksession on {file} and continue to keep
  it updated until Vim exits, triggering on the BufEnter and VimLeavePre
  autocommands. If the file exists, it will be overwritten if and only
  if it looks like a session files.
- `:Obsession {dir}`: invoke :Obsession on {dir}/Session.vim.
- `:Obsession` if session tracking is already in progress, pause
  it. Otherwise, resume tracking or create a new session in the current
  directory.
- `:Obsession!`: stop obsession and delete the underlying session file.
- Indicator: `S`: stop, `$`: running

### vim-rsi

- Readline key bindings
- `<C-a>`: go to beginning of line
- `<C-x><C-a>`: access Vim's built-in i_CTRL_A or c_CTRL_A.
- `<C-b>`: go backwards one character. On a blank line, delete it and go
  back to the previous line.
- `<C-d>`: delete character in front of cursor. Falls back to i_CTRL-D
  or c_CTRL-D at the end of the line.
- `<C-f>`: Move forward one character.
- `<C-e>`: Go to the end of line. Falls back to i_CTRL-E.
- `<C-t>`: Transpose two characters in command mode.
- `<M-BS>`: delete backward one word
- `<M-b>`: go backwards one word
- `<M-d>`: delete forwards one word
- `<M-f>`: go forwards one word
- `<M-n>`: c_<Down> or i_<Down>
- `<M-p>`: c_<Up> or i_<Up>

### vim-easy-align

- https://github.com/junegunn/vim-easy-align
- `:h easy-align`
- A Vim alignment plugin.
- An *alignment rule* is a predefined set of options for common
  alignment tasks, which is identified by a single character, such as
  `<Space>`, `=`, `:`, `.`, `|`, `&`, `#`, and `,`.

#### `<Plug>` mappings (interactive mode)

The recommended method is to use `<Plug>(EasyAlign)` mapping in normal and
visual mode. They are usually mapped to `ga`, but you can choose any key
sequences.

```vim
nmap ga <Plug>(EasyAlign)
xmap ga <Plug>(EasyAlign)
```

1. `ga` key in visual mode, or `ga` followed by a motion or a text
   object to start interactive mode
1. (Optional) Enter keys to cycle between alignment mode (left, right, or center)
1. (Optional) N-th delimiter (default: 1)
    - `1`         Around the 1st occurrences of delimiters
    - `2`         Around the 2nd occurrences of delimiters
    - ...
    - `*`         Around all occurrences of delimiters
    - `**`        Left-right alternating alignment around all delimiters
    - `-`         Around the last occurrences of delimiters (`-1`)
    - `-2`        Around the second to last occurrences of delimiters
    - ...
1. Delimiter key (a single keystroke; `<Space>`, `=`, `:`, `.`, `|`, `&`, `#`, `,`) or an arbitrary regular expression followed by `<CTRL-X>`

#### Regular expression vs. predefined rules

You can use regular expressions but it's usually much easier to use predefined
alignment rules that you can trigger with a single keystroke.

| Key       | Description/Use cases                                                |
| --------- | -------------------------------------------------------------------- |
| `<Space>` | General alignment around whitespaces                                 |
| `=`       | Operators containing equals sign (`=`, `==,` `!=`, `+=`, `&&=`, ...) |
| `:`       | Suitable for formatting JSON or YAML                                 |
| `.`       | Multi-line method chaining                                           |
| `,`       | Multi-line method arguments                                          |
| `&`       | LaTeX tables (matches `&` and `\\`)                                  |
| `#`       | Ruby/Python comments                                                 |
| `"`       | Vim comments                                                         |
| `<Bar>`   | Table markdown                                                       |

#### Examples using predefined rules

| Keystrokes   | Description                        | Equivalent command    |
| ------------ | ---------------------------------- | --------------------- |
| `<Space>`    | Around 1st whitespaces             | `:'<,'>EasyAlign\ `   |
| `2<Space>`   | Around 2nd whitespaces             | `:'<,'>EasyAlign2\ `  |
| `-<Space>`   | Around the last whitespaces        | `:'<,'>EasyAlign-\ `  |
| `-2<Space>`  | Around the 2nd to last whitespaces | `:'<,'>EasyAlign-2\ ` |
| `:`          | Around 1st colon (`key:  value`)   | `:'<,'>EasyAlign:`    |
| `<Right>:`   | Around 1st colon (`key : value`)   | `:'<,'>EasyAlign:>l1` |
| `=`          | Around 1st operators with =        | `:'<,'>EasyAlign=`    |
| `3=`         | Around 3rd operators with =        | `:'<,'>EasyAlign3=`   |
| `*=`         | Around all operators with =        | `:'<,'>EasyAlign*=`   |
| `**=`        | Left-right alternating around =    | `:'<,'>EasyAlign**=`  |
| `<Enter>=`   | Right alignment around 1st =       | `:'<,'>EasyAlign!=`   |
| `<Enter>**=` | Right-left alternating around =    | `:'<,'>EasyAlign!**=` |

Instead of finishing the alignment with a delimiter key, you can type in
a regular expression if you press `<CTRL-/>` or `<CTRL-X>`.

#### Alignment options in interactive mode

While in interactive mode, you can set alignment options using special shortcut
keys listed below. The meaning of each option will be described in
[the following sections](#alignment-options).

| Key       | Option             | Values                                                     |
|-----------|--------------------|------------------------------------------------------------|
| `CTRL-F`  | `filter`           | Input string (`[gv]/.*/?`)                                 |
| `CTRL-I`  | `indentation`      | shallow, deep, none, keep                                  |
| `CTRL-L`  | `left_margin`      | Input number or string                                     |
| `CTRL-R`  | `right_margin`     | Input number or string                                     |
| `CTRL-D`  | `delimiter_align`  | left, center, right                                        |
| `CTRL-U`  | `ignore_unmatched` | 0, 1                                                       |
| `CTRL-G`  | `ignore_groups`    | `[]`, `['String']`, `['Comment']`, `['String', 'Comment']` |
| `CTRL-A`  | `align`            | Input string (`/[lrc]+\*{0,2}/`)                           |
| `<Left>`  | `stick_to_left`    | `{ 'stick_to_left': 1, 'left_margin': 0 }`                 |
| `<Right>` | `stick_to_left`    | `{ 'stick_to_left': 0, 'left_margin': 1 }`                 |
| `<Down>`  | `*_margin`         | `{ 'left_margin': 0, 'right_margin': 0 }`                  |


### vim-unimpaired

- https://github.com/tpope/vim-unimpaired
- `:h unimpaired`
- Pairs of handy bracket mappings.

### vim-abolish

- https://github.com/tpope/vim-abolish
- `:h abolish`
- Easily search for, substitute, and abbreviate multiple variants of a
  word.
- Pattern:
    + `box{,es} => box, boxes, Box, Boxes, BOX, BOXES`
- Commands: 2 commands, :Abolish is more general, :Subvert is more
  concise.

```vim
:Abolish [options] {abbreviation} {replacement}
:Abolish -delete [options] {abbreviation}

:Abolish -search [options] {pattern}
:Subvert/{pattern}[/flags]
:Abolish!-search [options] {pattern}
:Subvert?{pattern}[?flags]

:Abolish -search [options] {pattern} {grep-arguments}
:Subvert /{pattern}/[flags] {grep-options}
:Abolish!-search [options] {pattern} {grep-arguments}
:Subvert!/{pattern}/[flags] {grep-options}

:[range]Abolish -substitute [options] {pattern} {replacement}
:[range]Subvert/{pattern}/{replacement}[/flags]
```


### vim-dispatch

- https://github.com/tpope/vim-dispatch
- `:h dispatch`
- Asynchronous build and test dispatcher.

### vim-matchup

- https://github.com/andymass/vim-matchup
- `:h matchup`
- Enhance the `%`
    + `%`: cycle back and forth on a recognized word.
    + `{count}%`: If {count} is less than 6, go forwards {count}.
    times. Otherwise, go to {count} percentage in the file (N%).
    + `g%`: similar `%` but also seeking forwards for matching words.
    + `[%`: go to [count]th previous outer open word.
    + `]%`: go to [count]th next outer close word.
    + `z%`: go to inside [count]th nearest block.
    + `a%`: any block, small nested blocks inside the open-close block.
    + `i%`: inside of an any block.
    + `ds%`: delete surrounding matching words.
    + `cs%`: change surrounding matching words.

### targets.vim

- https://github.com/wellle/targets.vim
- `:h targets`
- Add 5 different kinds of text objects
    + Pair text objects
    + Quote text objects
    + Separator text objects
    + Argument text objects
    + Tag text objects
- 5 types of matching
    + In object
    + An object
    + Inside object
    + Around object
    + Next and last (previous) object
- Normal text objects not next and last text objects, it triggers object
  seeking.

### vim-repeat

Support repeat a whole mapping.

### vim-tmux-focus-events

- Support FocusGained, FocusLost in tmux and iterm2.
- tmux configuration: `set -g focus-events on`

### vim-gutentags

#### Intro

- Universal ctags for macOS
    + https://github.com/universal-ctags/homebrew-universal-ctags
    + https://github.com/universal-ctags/ctags
- Exuberant ctags: `brew install ctags`
    + `man ctags` to learn more.
- `:GutentagsUpdate`: update the current tag file for the current
  buffer.
- `:GutentagsUpdate!`: update the current tags file with the whole
  projects instead of just the current buffer.
- `:GutentagsToggleEnabled`: disables and re-enables Gutentags.
- `:GutentagsToggleTrace`: to troubleshoot
- `:h gutentags` to learn more.


```vim
set statusline+=%{gutentags#statusline('[',']')}
" Activate Gutentags when opening a file that’s somewhere under a
" directory that contains a Makefile file or folder.
let g:gutentags_project_root = ['Makefile']
```

#### ctags in Vim

- ctags options

```sh
--recurse=yes
--exclude=.git
--exclude=vendor/*
--exclude=node_modules/*
--exclude=db/*
--exclude=log/*
```

- generate ctags for a project: `ctags .`
- ignore all ctags files

```sh
echo "tags" >> ~/.global_ignore
git config --global core.excludesfile $HOME/.global_ignore
```

- Key mappings

```help
Ctrl+] - go to definition
Ctrl+T \ C-o - Jump back from the definition.
Ctrl+W Ctrl+] - Open the definition in a horizontal split
g] - show matches of the tag `:tselect`

" Add these lines in vimrc
map <C-\> :tab split<CR>:exec("tag ".expand("<cword>"))<CR>
map <A-]> :vsp <CR>:exec("tag ".expand("<cword>"))<CR>

Ctrl+\ - Open the definition in a new tab
Alt+] - Open the definition in a vertical split
```

- Commands
    + `:tnext`, `:tprevious`, `:tfirst`, `:tlast`, `:ltag`, etc.

- To learn more: `:h ctags`, `:h tag`


### vim-surround

vim-surround is all about "surroundings": parentheses, brackets, quotes,
XML tags, and more. The plugin provides mappings to easily delete,
change and add such surroundings in pairs.

- `cs"<p>`: change surround " with <p> (anywhere in the surrounding)
    + `cs"'`: change surround " with '
    + `cst"`: change surround tag with " (<p> -> ")
- `ds"`: delete surround "
    + `dst`: delete surround tag
- `ysiw]`: yield surround inner word with ] (no surrounding spaces) (iw
  is text object)
    + `Hello world!` -> `[Hello] world!`
    + `ysiw[`: similar but with surrounding spaces
- `yss)`: yield surround line with )
    + `Hellow world` -> `(Hello world)`
- Visual mode: select the text then `S<tag ...>`
- If install `repeat.vim`, `.` will work with ds, cs, yss

### vim-gitgutter

- `]h` (custom mapping, original `]c`): next hunk
- `[h` : previous hunk
- `<Leader>hp`: previous hunk
- `<Leader>hs`: stage hunk (cannot unstage a staged hunk)
- `<Leader>hu`: undo hunk (careful)
- `<Leader>G`: update the gutter (:GitGutter)
- `<Leader>gf`: toggle folding for all unchanged lines (:GitGutterFold)
- Hunk Text objects
    + `ic`: operates on the current hunk's lines
    + `ac`: does the same but also includes trailing empty lines

```vim
"""" git-gutter mapping

" This mapping also works with vimdiff
nmap ]h <Plug>GitGutterNextHunk
nmap [h <Plug>GitGutterPrevHunk

" Update the gutter
nmap <Leader>G :GitGutter<CR>

" Toggle folding for all unchanged lines
nmap <Leader>gf :GitGutterFold<CR>

" Hunk text objects
omap ih <Plug>GitGutterTextObjectInnerPending
omap ah <Plug>GitGutterTextObjectOuterPending
xmap ih <Plug>GitGutterTextObjectInnerVisual
xmap ah <Plug>GitGutterTextObjectOuterVisual
```

- Cycle through hunks in all buffers

```vim
function! NextHunkAllBuffers()
  let line = line('.')
  GitGutterNextHunk
  if line('.') != line
    return
  endif

  let bufnr = bufnr('')
  while 1
    bnext
    if bufnr('') == bufnr
      return
    endif
    if !empty(GitGutterGetHunks())
      normal! 1G
      GitGutterNextHunk
      return
    endif
  endwhile
endfunction

function! PrevHunkAllBuffers()
  let line = line('.')
  GitGutterPrevHunk
  if line('.') != line
    return
  endif

  let bufnr = bufnr('')
  while 1
    bprevious
    if bufnr('') == bufnr
      return
    endif
    if !empty(GitGutterGetHunks())
      normal! G
      GitGutterPrevHunk
      return
    endif
  endwhile
endfunction

nmap ]H :call NextHunkAllBuffers()<CR>
nmap [H :call PrevHunkAllBuffers()<CR>
```



### fzf.vim

- `:h fzf`
- https://github.com/junegunn/fzf.vim
- Modify content in the command input
    + `alt+backspace`: delete word
    + `ctrl-u`: delete line
    + `ctrl-a`: beginning of the line
    + `ctrl-e`: end of the line

```vim
"""" fzf.vim configuration
" Customize fzf colors to match your color scheme
let g:fzf_colors =
\ { 'fg':      ['fg', 'Normal'],
  \ 'bg':      ['bg', 'Normal'],
  \ 'hl':      ['fg', 'Comment'],
  \ 'fg+':     ['fg', 'CursorLine', 'CursorColumn', 'Normal'],
  \ 'bg+':     ['bg', 'CursorLine', 'CursorColumn'],
  \ 'hl+':     ['fg', 'Statement'],
  \ 'info':    ['fg', 'PreProc'],
  \ 'border':  ['fg', 'Ignore'],
  \ 'prompt':  ['fg', 'Conditional'],
  \ 'pointer': ['fg', 'Exception'],
  \ 'marker':  ['fg', 'Keyword'],
  \ 'spinner': ['fg', 'Label'],
  \ 'header':  ['fg', 'Comment'] }

" Mapping selecting mappings
nmap <leader><tab> <plug>(fzf-maps-n)
xmap <leader><tab> <plug>(fzf-maps-x)
omap <leader><tab> <plug>(fzf-maps-o)

" Insert mode completion
imap <c-x><c-k> <plug>(fzf-complete-word)
" Advanced customization using autoload functions
" inoremap <expr> <c-x><c-k> fzf#vim#complete#word({'left': '15%'})
imap <c-x><c-f> <plug>(fzf-complete-path)
imap <c-x><c-j> <plug>(fzf-complete-file-rg)
imap <c-x><c-l> <plug>(fzf-complete-line)
```

### ultisnips

- https://github.com/SirVer/ultisnips
    + Snippets
- `:h UltiSnips` to learn how to create snippets
- `:h snippet-options`: control the behavior of the snippet.

#### Settings

- `<Tab>`: trigger the snippet and trigger jump forward
- `<BS>`: trigger jump backward

#### How to create a snippet

- Put snippet files in `~/.vim/UltiSnips/`
- `filetype.snippets`
    + `python.snippets`
    + `snippets.snippets`
    + `tex.snippets`
- Overview
    + Tab stops & placeholders: `$1` or `${1: some text}`
    + Mirrors: `$1`
    + Transformations: `${1/.*/Hello/g}`, `${Tabstop
    No/regex/replacement text/options}`
    + Interpolation:
        * Shell: `echo hi` or `#!/usr/bin/perl; print "Hello"`
        * VimL: `!v "1+2 = " . string(1+2)`
        * Python: `!p snip.rv = "Hello"`


### vim-snippets

#### Markdown

- Header:
    + Level 1: sec
    + Level 2: ssec
    + Level 3: sssec
    + Level 4: par
    + Level 5: spar
- Links:
    + Inline link: link
    + Reference link: refl
    + Image link: img
    + Footnote: fnt
- Code:
    + Code block: cbl
    + Inlinde code: ilc
- Text rendering:
    + Italic text: `*`
    + Bold text: `**`
    + Italic and bold text: `***`
- General:
    + date: date
    + time: time
    + date and exact time: datetime
    + date in ISO format: diso
- Table:
    + Table with 3 rows and 3 columns: tb3x3

### vim-markdown-toc

- `:GenTocGFM`: generates GFM-style TOC
    + `<Leader>mT`: markdown TOC
- `:RemoveToc`: remove the TOC
    + `<Leader>mut`: markdown undo TOC

### vim-markdown

#### Configuration

```vim
"""" vim-markdown configuration

" Follow named anchors
let g:vim_markdown_follow_anchor = 1

" Auto-write when following links
let g:vim_markdown_autowrite = 1

" Disable auto add bullet points
let g:vim_markdown_auto_insert_bullets = 0
let g:vim_markdown_new_list_item_indent = 0

" Enable TOC window auto-fit
let g:vim_markdown_toc_autofit = 1

" code blocks
let g:vim_markdown_conceal_code_blocks = 0

" disable header folding
let g:vim_markdown_folding_disabled = 1

" do not use conceal feature
let g:vim_markdown_conceal = 0

" disable math tex conceal feature
let g:tex_conceal = ""
let g:vim_markdown_math = 1

" support front matter of various format
let g:vim_markdown_frontmatter = 1  " for YAML format
let g:vim_markdown_toml_frontmatter = 1  " for TOML format
let g:vim_markdown_json_frontmatter = 1  " for JSON format
```

#### Mappings

- `ge`: open the link under the cursor in Vim for editing. Useful for
  relative Markdown links.
    + `<Plug>Markdown_EditUrlUnderCursor` can be used to change the
    mapping
- `gx`: open the link under the cursor in the same browser as the
  standard gx command.
    + `<Plug>Markdown_OpenUrlUnderCursor`
- `]]`: go to next header. <Plug>Markdown_MoveToNextHeader
- `[[`: go to previous header. <Plug>Markdown_MoveToPreviousHeader
- `][`: go to next sibling header if any. <Plug>Markdown_MoveToNextSiblingHeader
- `[]`: go to previous sibling header if any. <Plug>Markdown_MoveToPreviousSiblingHeader
- `]c`: go to Current header. <Plug>Markdown_MoveToCurHeader
- `]u`: go to parent header (Up). <Plug>Markdown_MoveToParentHeader

Custom mappings

```vim
"""" vim-markdown mapping
nmap <Leader>mf :TableFormat<CR>
xmap <Leader>mf :TableFormat<CR>
nmap <Leader>mt :Toc<CR>
xmap <Leader>mi :HeaderIncrease<CR>
xmap <Leader>md :HeaderDecrease<CR>
```


#### Commands

- `:HeaderDecrease`
    + Decrease level of all headers in buffer: h2 to h1, h3 to h2, etc.
    + If range is given, only operate in the range.
    + If an h1 would be decreased, abort.
- `:HeaderIncrease`
- `:SetexToAtx`: convert all Setex style headers in buffer to Atx.
     + Can operate on range
- `:TableFormat`: Format the table under the cursor
    + The input table must already have a separator line as the second
    line of the table. That line only needs to contain the correct pipes
    |.
- `:Toc`: create a quickfix vertical window navigable table of contents
  with the headers.
    + `:Toch`, `:Toct`, `:Tocv`


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

### vim-scriptease (debugging vim)

- The plugin helps making plugins
- Key mappings
    + `zS`: show the names of all syntax highlighting groups for the
      character under the cursor.
    + `{count}zS`: show the :syn-list for the {count}th syntax group
      under the cursor. 1zS shows the innermost group.
- `:Messages` capture the output of `:messages` and load it into the
  quickfix list.
    + All the messages that have shown in the bottom of vim at the
      status bar.
- `:Verbose <command>`: open a preview window to capture command's
  results (built-in alternative `:verbose <command>`)
    + `:verbose :com <command>`: show the last place that define the
      command.
- `:Scriptnames`: open a preview window to capture all the configuration
  files that Vim has loaded in order.

### fugitive-vim

- https://dev.to/iggredible/working-with-vim-and-git-4nkh

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
    + P   : reblame at [count]th parent (like `HEAD^[count]`)
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
- When browsing git objects and then open revisions of a file, we can
  use `:Gwrite` to checkout that particular revision of the file into
  the working copy.
    + `:Gwrite!`: force write
- Status line: show branch in the status line
    + `set statusline+=%{FugitiveStatusline()}`

### Colorscheme

- https://github.com/morhetz/gruvbox
    + Terminal specific: https://github.com/morhetz/gruvbox/wiki/Terminal-specific
    + iterm2, tmux
    + https://web.archive.org/web/20190121063455/https://medium.com/@dubistkomisch/how-to-actually-get-italics-and-true-colour-to-work-in-iterm-tmux-vim-9ebe55ebc2be
- https://vimcolorschemes.com/top

### Language pack

- https://github.com/sheerun/vim-polyglot
    + List of useful plugins

### Productivity

- https://vimawesome.com/plugin/vim-orgmode

### Completion

- Built-in manual completion: `:h ins-completion`
- Plugins
    + Convenience plugins: fallback completion sources, so you only need
    to memorize one key mapping.
        * https://github.com/ajh17/VimCompletesMe
        * https://github.com/lifepillar/vim-mucomplete
    + omnifunc plugins: add a source to omni completion
        * https://github.com/OmniSharp/omnisharp-vim
        * https://github.com/Quramy/tsuquyomi
        * https://github.com/justmao945/vim-clang
    + IDE-like plugins
        * https://github.com/prabirshrestha/asyncomplete.vim
        * https://github.com/maralla/completor.vim
        * https://github.com/Shougo/deoplete.nvim
        * https://github.com/Valloric/YouCompleteMe


Example configuration

Here comes with my configurations, if you want to give them a try:

.vimrc

```vim
set completeopt-=preview
set completeopt+=menu,menuone,noinsert,noselect
set shortmess+=c

augroup OmniCompletionSetup
    autocmd!
    autocmd FileType c          set omnifunc=ccomplete#Complete
    autocmd FileType php        set omnifunc=phpcomplete#CompletePHP
    autocmd FileType python     set omnifunc=jedi#completions
    autocmd FileType ruby       set omnifunc=rubycomplete#Complete
    autocmd FileType javascript set omnifunc=javascriptcomplete#CompleteJS
    autocmd FileType html       set omnifunc=htmlcomplete#CompleteTags
    autocmd FileType css        set omnifunc=csscomplete#CompleteCSS
    autocmd FileType xml        set omnifunc=xmlcomplete#CompleteTags
augroup END
```

YouCompleteMe.vim

```vim
let g:ycm_auto_trigger = 0  "Use <C-Space> to triggle YCM
let g:ycm_seed_identifiers_with_syntax = 1
let g:ycm_collect_identifiers_from_tags_files = 1

" Maybe we don't need this setting
let g:ycm_filetype_blacklist = {
      \ 'tagbar': 1,
      \ 'notes': 1,
      \ 'markdown': 1,
      \ 'netrw': 1,
      \ 'unite': 1,
      \ 'text': 1,
      \ 'vimwiki': 1,
      \ 'pandoc': 1,
      \ 'infolog': 1,
      \ 'mail': 1
      \}
```

neocomplete.vim

```vim
" Shortcut for toggle neocomplete
noremap <Leader>no :NeoCompleteToggle<CR>

" Use neocomplete
let g:neocomplete#enable_at_startup = 1

" Disable delay
let g:neocomplete#auto_complete_delay = 0

" Use smartcase
let g:neocomplete#enable_smart_case = 1

" Set minimum syntax keyword length
let g:neocomplete#sources#syntax#min_keyword_length = 3

" Define dictionary
let g:neocomplete#sources#dictionary#dictionaries = {
    \ 'default' : ''
    \ }

call neocomplete#custom#source('_', 'sorters', [])

" Define keyword
if !exists('g:neocomplete#keyword_patterns')
    let g:neocomplete#keyword_patterns = {}
endif
let g:neocomplete#keyword_patterns['default'] = '\h\w*'

" SuperTab like snippets behavior
imap <expr><TAB> pumvisible() ? "\<C-N>" : "\<TAB>"
smap <expr><TAB> pumvisible() ? "\<C-N>" : "\<TAB>"
imap <expr><S-TAB> pumvisible() ? "\<C-P>" : "\<S-TAB>"
smap <expr><S-TAB> pumvisible() ? "\<C-P>" : "\<S-TAB>"

" <CR>: close popup and save indent
inoremap <silent> <CR> <C-R>=<SID>ClosePopup()<CR>
function! <SID>ClosePopup()
    return pumvisible() ? "\<C-Y>" : "\<CR>"
endfunction

" Undo and manual completion
inoremap <expr><C-G> neocomplete#undo_completion()
inoremap <expr><C-L> neocomplete#complete_common_string()

" Enable heavy omni completion
if !exists('g:neocomplete#sources#omni#input_patterns')
    let g:neocomplete#sources#omni#input_patterns = {}
endif
let g:neocomplete#sources#omni#input_patterns.php = '\h\w\{1,}\|[^. \t]->\%(\h\w*\)\?\|\h\w*::\%(\h\w*\)\?'
let g:neocomplete#sources#omni#input_patterns.python = '\%([^. \t]\.\|^\s*@\|^\s*from\s.\+import \|^\s*from \|^\s*import \)\w*'
let g:neocomplete#sources#omni#input_patterns.ruby = '[^. *\t]\.\w*\|\h\w*::'
let g:neocomplete#sources#omni#input_patterns.perl = '[^. \t]->\%(\h\w*\)\?\|\h\w*::\%(\h\w*\)\?'

if !exists('g:neocomplete#force_omni_input_patterns')
    let g:neocomplete#force_omni_input_patterns = {}
endif

" Manual omni completion
inoremap <expr><C-F> neocomplete#start_manual_complete()
```


completor.vim

```vim
let g:completor_php_omni_trigger = '([$\w]{2,}|use\s*|->[$\w]*|::[$\w]*|implements\s*|extends\s*|class\s+[$\w]+|new\s*)$'

imap <expr><TAB> pumvisible() ? "\<C-N>" : "\<TAB>"
smap <expr><TAB> pumvisible() ? "\<C-N>" : "\<TAB>"
imap <expr><S-TAB> pumvisible() ? "\<C-P>" : "\<S-TAB>"
smap <expr><S-TAB> pumvisible() ? "\<C-P>" : "\<S-TAB>"
imap <expr><CR> pumvisible() ? "\<C-Y>\<CR>" : "\<CR>"
smap <expr><CR> pumvisible() ? "\<C-Y>\<CR>" : "\<CR>"
```

vim-mucomplete.vim

```vim
let g:mucomplete#enable_auto_at_startup = 1

let g:mucomplete#chains = {}
let g:mucomplete#chains.default = ['file', 'omni', 'keyn', 'dict', 'ulti']
let g:mucomplete#chains.unite = []
```

PS. You also need to install related omni completion plugins.


## Key mapping

### Overview about key mapping

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

- Resources
    + https://vi.stackexchange.com/questions/10249/what-is-the-difference-between-mapped-key-sequences-and-key-codes-timeoutl#answer-10284
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

## File type specific configurations

- https://www.reddit.com/r/vim/wiki/where_to_put_filetype_specific_stuff
- https://vi.stackexchange.com/questions/8056/for-an-autocmd-in-a-ftplugin-should-i-use-pattern-matching-or-buffer

### If Vim know the file type

- Tell Vim to detect the file type and apply the configuration
    + `filetype plugin indent on` in your `.vimrc`

When Vim recognizes a known filetype it sets the filetype option and
emits the FileType event, which itself triggers the sourcing of the
corresponding filetype plugins. Filetype plugins are sourced in that
order:

1. `~/.vim/ftplugin/<filetype>.vim`

This is the most obvious location but also the most susceptible to be
overridden by system defaults. If you want to disable other filetype
plugins, put the following check in the beginning of your
`<filetype>.vim`:

```vim
" Only do this when not done yet for this buffer
if exists("b:did_ftplugin")
  finish
endif
let b:did_ftplugin = 1
```


2. `$VIMRUNTIME/ftplugin/<filetype>.vim`

This one is in Vim's system-wide runtime so it will load other filetype
plugins.

3. `~/.vim/after/ftplugin/<filetype>.vim`

This one is always sourced last so options and commands are guaranteed
to take precedence over system defaults. Bingo! Don't put the check of
`b:did_ftplugin` here to add your own configurations.

> The important of undoing, when the file is set to other filetype, you
>    need to undo your configurations. You can do that by set the
>    `b:undo_ftplugin` string.

From there, you only need to:

create `~/.vim/after/ftplugin/<filetype>.vim` if it doesn't already exist,

and put your options and stuff in that file.

Example for the foo filetype:

```vim
" Uncomment following lines if you want to disable other filetype
" plugins
" Only do this when not done yet for this buffer
" if exists("b:did_ftplugin")
"   finish
" endif
" let b:did_ftplugin = 1

setlocal expandtab
setlocal shiftwidth=7
nnoremap <buffer> <F5> :echo 'I pressed F5 in a foo file!'<CR>

" If you use autocmd in this plugin, you need to put it in an augroup
" and clear the previous autocmd's using au! * <buffer>
augroup my_filetype
    au! * <buffer>  "Clear all previous autocmd's for this buffer

    " If you want to set options for each window (not buffer, many
    " windows can show the same buffer) then you need to set it here
    " using autocmd with BufWinEnter event.
    au BufWinEnter <buffer> setlocal list
augroup END

" Append the undo string
" Using ":setlocal" with "<" after the option name resets the option to
" its global value.  That is mostly the best way to reset the option
" value.
let b:undo_ftplugin .= "setlocal expandtab< shiftwidth<"
    \ . "| nunmap <buffer> <F5>"
```

### If Vim does not know the file type

- Tell Vim how to detect the file

This is done with a filetype detection script in `~/.vim/ftdetect/`:

```vim
" ~/.vim/ftdetect/foo.vim
" You don't need to wrap autocmd in an augroup since Vim does it by
" itself :h ftdetect
autocmd BufNewFile,BufRead *.foo setf foo
```

Once that file exists, it will be sourced on every startup and allow Vim
to assign filetype foo to every file with extension .foo.

Alternatively, you could put that autocommand in your vimrc.

```vim
"Standard" form:

augroup my_fancy_filetypes
    autocmd!
    autocmd BufNewFile,BufRead *.foo setf foo
augroup END
```

### Local and global settings

Be careful about the options you set and the mappings you create.

Some options are buffer-local, some others are buffer-or-window-local,
some others are global, and most global options can have a local
value. If you don't want your language-specific options to leak into
other filetypes you must set them as locally as possible:

```vim
setlocal expandtab
```

Similarly, mappings are global by default but can be made buffer-local
by adding the <buffer> argument:

```vim
nnoremap <buffer> <key> :echo "I pressed a key!"<CR>
```

This also applies to Ex commands:

```vim
command! -buffer Foo echo "Foo bar baz"
```


## Vim script

Vim script (`viml`) is the scripting language built into Vim. Based on
the ex editor language of the original vi editor.

Vim script files are stored in plain text format and the file name
extension is `.vim`.

# Theme, interface

## Status line

```vim
"""" Statusline
set laststatus=2                "Always show the status line at the bottom
set statusline=
set statusline+=%#PmenuSel#     "Highlight the git branch
set statusline+=%{FugitiveStatusline()} "Git branch of this file
set statusline+=%{ObsessionStatus()}    "Indicator for sessions: 'S': stop, '$': running
set statusline+=%#LineNr#       "Erase highlight for other parts
set statusline+=\ %f            "A whitespace followed by file path
set statusline+=%m              "Modified flag
set statusline+=%=              "Separation point between left and right items
set statusline+=\ %y            "A whitespace followed by file type
set statusline+=\ %{&fileencoding?&fileencoding:&encoding} "File encoding
set statusline+=\ [%{&fileformat}]   "File format: unix, dos, mac
set statusline+=\ %p%%          "Percentage through file in lines
set statusline+=\ %l:%c         "Line and column numbers
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
- Location list: the local quickfix list for each window
    + `:lopen`, `:lclose`, `:lprevious`, `:lnext`, `:lfirst`, `:llast`
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

# Vim's pipes

- `:write`, `:read`, `:filter`
- `:h shellpipe`

# Compile, build, lint

- https://gist.github.com/ajh17/a8f5f194079818b99199
- `:h make`

# Registers

- https://stackoverflow.com/a/3997110/1683888

# Macros

- https://gist.github.com/romainl/9721c7dd13c30714f568063e03c106dd


## How to store a macro?

### In a register

#### via recording

    qa                 " start recording in register a
    2wcefoobar<Esc>    " do your thing
    q                  " stop recording

#### via assignation

    " put 2wcefoobar<Esc> in register k
    let @k = "2wcefoobar\<Esc>"

Note the use of double quotes that allows us to use `\<Esc>` rather than
the slightly harder to reason about `^[`.

#### via yanking

    " yank visual selection to register z
    "zy

### In a variable

    " put 2wcefoobar\<Esc> in variable myvar
    let myvar = "2wcefoobar\<Esc>"

### In a mapping

    " map <key> to 2wcefoobar<Esc> in normal mode
    nnoremap <key> 2wcefoobar<Esc>

### In an Ex command

    " create an Ex command :Foo that does 2wcefoobar<Esc>
    command! Foo normal! 2wcefoobar<Esc>

### In a function

    " create a function Foo() that does 2wcefoobar<Esc>
    function! Foo()
        normal! 2w
        normal! cefoobar
    endfunction

## How to play a macro back?

Some macros may start from visual mode, others work on lines, others can
have nothing to do with editing text, and each macro can be stored in
various ways… so how to play a given macro back usually depends on what
the macro does, where it is stored, what mode we are in, where the
cursor is right now, and where the cursor lands at the end of the
playback.

If we forget functions, Ex commands, and mappings for a moment, we
basically have two playback methods at our disposal:

* executing the content of a register right *here*,
* executing the content of a register from column 0 of every line in a
  given range.
    - https://stackoverflow.com/questions/390174/in-vim-how-do-i-apply-a-macro-to-a-set-of-lines

Command                          | Description
---------------------------------|-------------------------------------------------------------------------
`[n]@<register>`                 | execute content of `<register>` `[n]` times
`:[range]normal! [n]@<register>` | execute content of `<register>` `[n]` times on every line in `[range]`

The mechanism is the same whether the macro we want to play back is
stored in a register or in a variable. In one case we use the register
itself, directly. In the other case we use the expression register that
we fill with the content of our variable:

With a register (say `q`), we would do:

    @q
    12@q
    :7,23norm! @q

With a variable (say `foo`), we would do:

    @=foo<CR>
    3@=foo<CR>
    :'{,'}norm! @=foo<CR>

## How to edit a macro?

Macros being plain text, editing a macro is as simple as putting it into
a buffer, editing it, and storing it again in the same box or another
one.

Say we recorded this simple macro in register `q`:

    dw

but we figure out that some of the words we want to cut are actually
WORDS. The obvious solution is to change `dw` into `dW`.

1. Put the content of register `q` right here in a new buffer:

        <C-w>n
        "qp

2. Edit it:

        ~

3. Cut it back to register `q`:

        v0"qd

   or:

        :let @q = getline('.')

Done.

If you are working with a variable (say `foo`):

```
:new
:put=foo
~
:let foo = getline('.')
```

And that's about all you need to know for your day-to-day use of macros.

## Mappings and functions.

Most macros are short-lived because they tend to be contextual by nature
but some others are generic enough to find their way in our
workflow. Those generally useful macros could certainly be stored and
used *as-is*, but there's certainly an opportunity, here, to make them a
little bit smarter and future-proof.

We are going to work with this simple macro that inserts a debugging
statement containing the word under the cursor below the current line:

    yiwoconsole.log("<C-r>"", <C-r>");<Esc>

If we don't want to clobber registers and we think variables are not
really useful we can still turn that macro into a mapping:

    nnoremap <key> yiwoconsole.log("<C-r>"", <C-r>");<Esc>

But we are still clobbering the unnamed register and we don't really
want to clobber *any* register, do we? Let's try to turn this "dumb"
macro into a "smart" function.

# Troubleshooting

## Showing messages to debug

- `:mess`, `:messages`, or enhanced `:Messages` from the plugin
  `vim-scriptease`

## Error: * not found *

- Check runtime path: `:set runtimepath?`

## Debugging Vim Scripts

- https://codeinthehole.com/tips/debugging-vim-by-example/

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

[wiki]: https://en.wikipedia.org/wiki/Vim_(text_editor)
[1]: http://vimcasts.org/episodes/the-file-explorer/ "Vimcasts - 15. The file explorer"
[plugins]: https://vimawesome.com/
