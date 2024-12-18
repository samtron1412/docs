[TOC]

# Overview

# Tips and Tricks

## Add and edit Snippets

- Preferences > Shortcut > Snippets
    + Add/remove/export/import snippets
- Use `Toolbelt` to display Snippets
    + Select `Snippets` under Toolbelt
    + Use shortcut to open the toolbelt
- Edits > Snippets
    + Use snippets
- Configure the status bar of the profiles to send snippets
    + Preferences > Profiles > Session > Status bar enabled > Configure status bar > Send Snippet

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

## Cursor style

- iterm2 > Preferences > Profiles > Colors
    + Uncheck Cursor guide: cursor line
    + Smart box cursor color
- iterm2 > Preferences > Profiles > Text
    + Uncheck blinking cursor
    + Shape: Vertical bar
