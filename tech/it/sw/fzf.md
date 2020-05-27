[toc]

# Overview


# Introduction

- `man fzf`
- `find * -type f | fzf > selected`
    + fzf will launch an interactive finder
    + read the list from STDIN
    + and write the selected item to STDOUT
- Without the STDIN pipe, fzf will use find command to fetch the list of
  files excluding hidden ones.
    + You can override the default command with `FZF_DEFAULT_COMMAND`
    environment variable.
- `vim $(fzf)`
    + Using fzf to find the file and open it using Vim

# Using the finder

- CTRL-J / CTRL-K (or CTRL-N / CTRL-P) to move cursor up and down
- Enter key to select the item, CTRL-C / CTRL-G / ESC to exit
- On multi-select mode (-m), TAB and Shift-TAB to mark multiple items
- Emacs style key bindings
- Mouse: scroll, click, double-click; shift-click and shift-scroll on
  multi-select mode

# Layout

fzf by default starts in fullscreen mode, but you can make it start
below the cursor with --height option.

`vim $(fzf --height 40%)`

Also check out --reverse and --layout options if you prefer "top-down"
layout instead of the default "bottom-up" layout.

`vim $(fzf --height 40% --reverse)`

You can add these options to `$FZF_DEFAULT_OPTS` so that they're applied
by default. For example,

```sh
export FZF_DEFAULT_OPTS='--height 40% --layout=reverse --border'
```

# Search syntax

| Token     | Match type                 | Description                          |
| --------- | -------------------------- | ------------------------------------ |
| `sbtrkt`  | fuzzy-match                | Items that match `sbtrkt`            |
| `'wild`   | exact-match (quoted)       | Items that include `wild`            |
| `^music`  | prefix-exact-match         | Items that start with `music`        |
| `.mp3$`   | suffix-exact-match         | Items that end with `.mp3`           |
| `!fire`   | inverse-exact-match        | Items that do not include `fire`     |
| `!^music` | inverse-prefix-exact-match | Items that do not start with `music` |
| `!.mp3$`  | inverse-suffix-exact-match | Items that do not end with `.mp3`    |

If you don't prefer fuzzy matching and do not wish to "quote" every word,
start fzf with `-e` or `--exact` option. Note that when  `--exact` is set,
`'`-prefix "unquotes" the term.

A single bar character term acts as an OR operator. For example, the following
query matches entries that start with `core` and end with either `go`, `rb`,
or `py`.

```
^core go$ | rb$ | py$
```

# Environment variables

- `FZF_DEFAULT_COMMAND`
    - Default command to use when input is tty
    - e.g. `export FZF_DEFAULT_COMMAND='fd --type f'`
- `FZF_DEFAULT_OPTS`
    - Default options
    - e.g. `export FZF_DEFAULT_OPTS="--layout=reverse --inline-info"`

# Options

See the man page (`man fzf`) for the full list of options.

# Demo

- https://www.youtube.com/watch?v=qgG5Jhi_Els

# Examples

## Key bindings for command line

- CTRL-T - Paste the selected files and directories onto the command-line
    + Set FZF_CTRL_T_COMMAND to override the default command
    + Set FZF_CTRL_T_OPTS to pass additional options
- CTRL-R - Paste the selected command from history onto the command-line
    + If you want to see the commands in chronological order, press
    CTRL-R again which toggles sorting by relevance
    + Set FZF_CTRL_R_OPTS to pass additional options
- ALT-C - cd into the selected directory
    + Set FZF_ALT_C_COMMAND to override the default command
    + Set FZF_ALT_C_OPTS to pass additional options

## Files and directories

Fuzzy completion for files and directories can be triggered if the word
before the cursor ends with the trigger sequence which is by default `**.

`COMMAND [DIRECTORY/][FUZZY_PATTERN]**<TAB>

```sh
# Files under current directory
# - You can select multiple items with TAB key
vim **<TAB>

# Files under parent directory
vim ../**<TAB>

# Files under parent directory that match `fzf`
vim ../fzf**<TAB>

# Files under your home directory
vim ~/**<TAB>


# Directories under current directory (single-selection)
cd **<TAB>

# Directories under ~/github that match `fzf`
cd ~/github/fzf**<TAB>
```

## Process IDs

Fuzzy completion for PIDs is provided for kill command. In this case,
there is no trigger sequence, just press tab key after kill command.

```sh
# Can select multiple processes with <TAB> or <Shift-TAB> keys
kill -9 <TAB>
```

## Host names

For ssh and telnet commands, fuzzy completion for host names is provided. The
names are extracted from /etc/hosts and ~/.ssh/config.

```sh
ssh **<TAB>
telnet **<TAB>
```

## Environment variables / Aliases

```sh
unset **<TAB>
export **<TAB>
unalias **<TAB>
```

## Settings

```sh
# Use ~~ as the trigger sequence instead of the default **
export FZF_COMPLETION_TRIGGER='~~'

# Options to fzf command
export FZF_COMPLETION_OPTS='+c -x'

# Use fd (https://github.com/sharkdp/fd) instead of the default find
# command for listing path candidates.
# - The first argument to the function ($1) is the base path to start traversal
# - See the source code (completion.{bash,zsh}) for the details.
_fzf_compgen_path() {
  fd --hidden --follow --exclude ".git" . "$1"
}

# Use fd to generate the list for directory completion
_fzf_compgen_dir() {
  fd --type d --hidden --follow --exclude ".git" . "$1"
}
```

## Supported commands

On bash, fuzzy completion is enabled only for a predefined set of commands
(`complete | grep _fzf` to see the list). But you can enable it for other
commands as well as follows.

```sh
complete -F _fzf_path_completion -o default -o bashdefault ag
complete -F _fzf_dir_completion -o default -o bashdefault tree
```


