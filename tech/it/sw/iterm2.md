[TOC]

# Overview

# Tips and Tricks

## Starting tmux automatically

- iterm2 > Preferences > Profiles > Default > General > Command
    + Send text as start: `tmux ls && read tmux_session && tmux attach -t ${tmux_session:-default} || tmux new -s ${tmux_session:-default}`
    + This command will create a default tmux session at the first run
      of iterm2. In the next run, it will show the list of tmux sessions
      so that users can choose an existing tmux session by typing its
      name or create a new one by typing a new name.

## Window style

- iterm2 > Preferences > Profiles > Default > Window
    + Style: Full-Height Right of Screen
    + Screen: No preference
    + Space: Current Space
