[TOC]

# Overview

A minimalist vim plugin manager.

# Installation, Update, Remove

- Download `plug.vim` and put it in the `autoload` directory

```Unix
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

- Update: `:PlugUpgrade`
- Remove:
    + Delete the `plug.vim` file in `~/.vim/autoload`
    + Delete the vim-plug section in `.vimrc`

# Usage

## Overview

Add a vim-plug section to your ~/.vimrc (or ~/.config/nvim/init.vim
for Neovim):
- Begin the section with `call plug#begin()`
- List the plugins with `Plug` commands
- `call plug#end()` to update `&runtimepath` and initialize plugin system
    + Automatically executes `filetype plugin indent on` and `syntax
      enable`. You can revert the settings after the call. e.g.
      `filetype indent off`, `syntax off`, etc.

```example
" Specify a directory for plugins
" - For Neovim: ~/.local/share/nvim/plugged
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.vim/plugged')

" Make sure you use single quotes

" Shorthand notation; fetches https://github.com/junegunn/vim-easy-align
Plug 'junegunn/vim-easy-align'

" Any valid git URL is allowed
Plug 'https://github.com/junegunn/vim-github-dashboard.git'

" Multiple Plug commands can be written in a single line using | separators
Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

" On-demand loading
Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Using a non-master branch
Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

" Using a tagged release; wildcard allowed (requires git 1.9.2 or above)
Plug 'fatih/vim-go', { 'tag': '*' }

" Plugin options
Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }

" Plugin outside ~/.vim/plugged with post-update hook
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }

" Unmanaged plugin (manually installed and updated)
Plug '~/my-prototype-plugin'

" Initialize plugin system
call plug#end()
```

- Reload `.vimrc` and `:PlugInstall` to install plugins.
- Update plugins: `:PlugUpdate`
    + See the differences and roll back: `:PlugDiff`
    + Roll back by pressing `X` (capital X)
- Remove a plugin
    + Delete or comment out the Plug command in .vimrc
    + Reload vimrc or restart Vim
    + `:PlugClean`

## Commands

| Command                           | Description                                                        |
| -                                 | -                                                                  |
| PlugInstall [name ...] [#threads] | Install plugins                                                    |
| PlugUpdate [name ...] [#threads]  | Install or update plugins                                          |
| PlugClean[!]                      | Remove unused directories (bang version will clean without prompt) |
| PlugUpgrade                       | Upgrade vim-plug itself                                            |
| PlugStatus                        | Check the status of plugins                                        |
| PlugDiff                          | Examine changes from the previous update and the pending changes   |
| PlugSnapshot[!] [output path]     | Generate script for restoring the current snapshot of the plugins  |

## Plug options

| Option            | Description                                    |
| -                 | -                                              |
| branch/tag/commit | Branch/tag/commit of the repository to use     |
| rtp               | Subdirectory that contains Vim plugin          |
| dir               | Custom directory for the plugin                |
| as                | Use different name for the plugin              |
| do                | Post-update hook (string or funcref)           |
| on                | On-demand loading: Commands or <Plug>-mappings |
| for               | On-demand loading: File types                  |
| frozen            | Do not update unless explicitly specified      |

## Global options

| Flag              | Default                         | Description                                                                    |
| -                 | -                               | -                                                                              |
| g:plug_threads    | 16                              | Default number of threads to use                                               |
| g:plug_timeout    | 60                              | Time limit of each task in seconds (Ruby & Python)                             |
| g:plug_retries    | 2                               | Number of retries in case of timeout (Ruby & Python)                           |
| g:plug_shallow    | 1                               | Use shallow clone                                                              |
| g:plug_window     | vertical topleft new            | Command to open plug window                                                    |
| g:plug_pwindow    | above 12new                     | Command to open preview window in PlugDiff                                     |
| g:plug_url_format | https://git::@github.com/%s.git | printf format to build repo URL (Only applies to the subsequent Plug commands) |

## Keybindings

D - PlugDiff
S - PlugStatus
R - Retry failed update or installation tasks
U - Update plugins in the selected range
q - Close the window
:PlugStatus
L - Load plugin
:PlugDiff
X - Revert the update

## On-demand loading of plugins

"Premature optimization is the root of all evil."

You most likely don't need them at all. A properly implemented Vim
plugin should already load lazily without any help from the plugin
manager (:help autoload). There are very few cases where those options
actually make much sense. On-demand loading should only be used as the
last resort. It is basically a hacky workaround and is not always
guaranteed to work.

Before applying the options, make sure that you're tackling the right
problem by breaking down the startup of time of Vim using --startuptime.
See if there are plugins that take more than a few milliseconds to load.

```bash
vim --startuptime /tmp/log
```

```
" NERD tree will be loaded on the first invocation of NERDTreeToggle command
Plug 'scrooloose/nerdtree', { 'on': 'NERDTreeToggle' }

" Multiple commands
Plug 'junegunn/vim-github-dashboard', { 'on': ['GHDashboard', 'GHActivity'] }

" Loaded when clojure file is opened
Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Multiple file types
Plug 'kovisoft/paredit', { 'for': ['clojure', 'scheme'] }

" On-demand loading on both conditions
Plug 'junegunn/vader.vim',  { 'on': 'Vader', 'for': 'vader' }

" Code to execute when the plugin is lazily loaded on demand
Plug 'junegunn/goyo.vim', { 'for': 'markdown' }
autocmd! User goyo.vim echom 'Goyo is now loaded!'
```

## Post-update hooks

There are some plugins that require extra steps after installation or
update. In that case, use `do` option to describe the task to be
performed.

```vim
Plug 'Shougo/vimproc.vim', { 'do': 'make' }
Plug 'Valloric/YouCompleteMe', { 'do': './install.py' }
```

If the value starts with `:`, it will be recognized as a Vim command.

```vim
Plug 'fatih/vim-go', { 'do': ':GoInstallBinaries' }
```

If you need more control, you can pass a reference to a Vim function
that takes a single argument.

```vim
function! BuildYCM(info)
  " info is a dictionary with 3 fields
  " - name:   name of the plugin
  " - status: 'installed', 'updated', or 'unchanged'
  " - force:  set on PlugInstall! or PlugUpdate!
  if a:info.status == 'installed' || a:info.force
    !./install.py
  endif
endfunction

Plug 'Valloric/YouCompleteMe', { 'do': function('BuildYCM') }
```

Both forms of post-update hook are executed inside the directory of the
plugin and only run when the repository has changed, but you can force
it to run unconditionally with the bang-versions of the commands:
`PlugInstall!` and `PlugUpdate!`.

Make sure to escape BARs and double-quotes when you write `do` option
inline as they are mistakenly recognized as command separator or the
start of the trailing comment.

```vim Plug 'junegunn/fzf', { 'do': 'yes \| ./install' }
```

But you can avoid the escaping if you extract the inline specification
using a variable (or any Vimscript expression) as follows:

```vim let g:fzf_install = 'yes | ./install' Plug 'junegunn/fzf', {
'do': g:fzf_install }
```

## `PlugInstall!` and `PlugUpdate!`

The installer takes the following steps when installing/updating a
plugin:

1. `git clone` or `git fetch` from its origin
2. Check out branch, tag, or commit and optionally `git merge` remote
   branch
3. If the plugin was updated (or installed for the first time) 1. Update
   submodules 2. Execute post-update hooks

The commands with `!` suffix ensure that all steps are run
unconditionally.

## Loading plugins manually

With on and for options, vim-plug allows you to defer loading of
plugins. But if you want a plugin to be loaded on an event that is not
supported by vim-plug, you can set on or for option to an empty list,
and use plug#load(names...) function later to load the plugin manually.
The following example will load ultisnips and YouCompleteMe first time
you enter insert mode.

```vim
" Load on nothing
Plug 'SirVer/ultisnips', { 'on': [] }
Plug 'Valloric/YouCompleteMe', { 'on': [] }

augroup load_us_ycm
  autocmd!
  autocmd InsertEnter * call plug#load('ultisnips', 'YouCompleteMe')
                     \| autocmd! load_us_ycm
augroup END
```

## Manage Dependencies

vim-plug no longer handles dependencies between plugins and it's up to
the user to manually specify Plug commands for dependent plugins.

```vim
Plug 'SirVer/ultisnips'
Plug 'honza/vim-snippets'
```

Some users prefer to use | separators or arbitrary indentation to
express plugin dependencies in their configuration files.

```vim
" Vim script allows you to write multiple statements in a row using `|` separators
" But it's just a stylistic convention. If dependent plugins are written in a single line,
" it's easier to delete or comment out the line when you no longer need them.
Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'
Plug 'junegunn/fzf', { 'do': './install --all' } | Plug 'junegunn/fzf.vim'

" Using manual indentation to express dependency
Plug 'kana/vim-textobj-user'
  Plug 'nelstrom/vim-textobj-rubyblock'
  Plug 'whatyouhide/vim-textobj-xmlattr'
  Plug 'reedes/vim-textobj-sentence'
```

- Ordering of plugins only matters when overriding an earlier plugin's
  commands or mappings, so putting the dependency next to the plugin
  that depends on it or next to other plugins' dependencies are both
  okay.
- In the rare case where plugins do overwrite commands or mappings,
  vim-plug requires you to manually reorder your plugins.

# Troubleshooting

## Color scheme

- Load color scheme after `call plug#end()` (activate the plugin before
  load color scheme)

## Installing YouCompleteMe manually

- The YCM plugin is to big to manage by this plugin manager
