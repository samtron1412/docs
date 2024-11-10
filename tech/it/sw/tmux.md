[TOC]

# Overview

- Books
    + https://leanpub.com/the-tao-of-tmux/read
- https://github.com/gpakosz/.tmux
- Pair programming: https://github.com/zolrath/wemux/

# Configuration

- User-specific configuration: `~/.tmux.conf`
- Global configuration: `/etc/tmux.conf`

- https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/
- color
    + https://superuser.com/questions/285381/how-does-the-tmux-color-palette-work

# Plugins

## Tmux Plugin Manager (tpm)

- https://github.com/tmux-plugins/tpm

## Tmux Resurrect

- https://github.com/tmux-plugins/tmux-resurrect
- `ctrl+b, ctrl+s`: save
- `ctrl+b, ctrl+r`: restore

# Cheatsheet

## Common

start new:

    tmux

start new with session name:

    tmux new -s myname

detach session:

		`ctrl+b d` or `ctrl+b :detach`

attach:

    tmux a  #  (or at, or attach)

attach to named:

    tmux a -t myname

list sessions:

    tmux ls

<a name="killSessions"></a>kill session:

    tmux kill-session -t myname

<a name="killAllSessions"></a>Kill all the tmux sessions:

    tmux ls | grep : | cut -d. -f1 | awk '{print substr($1, 0, length($1)-1)}' | xargs kill

In tmux, hit the prefix `ctrl+b` and then:

## Sessions

    :new<CR>  new session
    s  list sessions and switch between sessions
    $  name session

## Windows (tabs)

    c  new window
    w  list windows
    f  find window
    ,  name window
    &  kill window with confirmation

## Panes (splits)

    %  vertical split
    "  horizontal split

    x  kill pane with confirmation
    +  break pane into window (e.g. to select text by mouse to copy)
    -  restore pane from window
    ⍽  space - toggle between layouts
    <prefix> z toggle pane zoom

### Switching between panes

```
<prefix> o  cycle through panes
<prefix> q (Show pane numbers, when the numbers show up type the key to goto that pane)
<prefix> { (Move the current pane left)
<prefix> } (Move the current pane right)
<prefix> left       go to the next pane on the left
<prefix> right      (or one of these other directions)
<prefix> up
<prefix> down
<prefix> ;          go to the ‘last’ (previously used) pane
```

### Moving panes around

```
<prefix> {          move the current pane to the previous position
<prefix> }          move the current pane to the next position
<prefix> C-o        rotate window ‘up’ (i.e. move all panes)
<prefix> M-o        rotate window ‘down’
<prefix> !          move the current pane into a new separate
               window (‘break pane’)
<prefix> :move-pane -t :3.2
               split window 3's pane 2 and move the current pane there
```

## Sync Panes

You can do this by switching to the appropriate window, typing your Tmux
prefix (commonly Ctrl-B or Ctrl-A) and then a colon to bring up a Tmux
command line, and typing:

```
:setw synchronize-panes
```

You can optionally add on or off to specify which state you want;
otherwise the option is simply toggled. This option is specific to one
window, so it won’t change the way your other sessions or windows
operate. When you’re done, toggle it off again by repeating the command.
[tip source](http://blog.sanctum.geek.nz/sync-tmux-panes/)


## Resizing Panes

You can also resize panes if you don’t like the layout defaults. I
personally rarely need to do this, though it’s handy to know how. Here
is the basic syntax to resize panes:

    PREFIX : resize-pane -D (Resizes the current pane down)
    PREFIX : resize-pane -U (Resizes the current pane upward)
    PREFIX : resize-pane -L (Resizes the current pane left)
    PREFIX : resize-pane -R (Resizes the current pane right)
    PREFIX : resize-pane -D 20 (Resizes the current pane down by 20 cells)
    PREFIX : resize-pane -U 20 (Resizes the current pane upward by 20 cells)
    PREFIX : resize-pane -L 20 (Resizes the current pane left by 20 cells)
    PREFIX : resize-pane -R 20 (Resizes the current pane right by 20 cells)
    PREFIX : resize-pane -t 2 20 (Resizes the pane with the id of 2 down by 20 cells)
    PREFIX : resize-pane -t -L 20 (Resizes the pane with the id of 2 left by 20 cells)


## Copy mode:

Pressing `PREFIX [` places us in Copy mode.

- Default mode keys is `vi`
    + `setw -g mode-keys vi`

To get out of Copy mode, we just press the `ENTER` key.

       Function                vi             emacs

       Start selection         Space          C-Space
       Select whole line       V
       Back to indentation     ^              M-m
       Clear selection         Escape         C-g
       Copy selection          Enter          M-w
       Cursor down             j              Down
       Cursor left             h              Left
       Cursor right            l              Right
       Cursor to bottom line   L
       Cursor to middle line   M              M-r
       Cursor to top line      H              M-R
       Cursor up               k              Up
       Delete entire line      d              C-u
       Delete to end of line   D              C-k
       End of line             $              C-e
       Goto line               :              g
       Half page down          C-d            M-Down
       Half page up            C-u            M-Up
       Next page               C-f            Page down
       Next word               w              M-f
       Paste buffer            p              C-y
       Previous page           C-b            Page up
       Previous word           b              M-b
       Quit mode               q              Escape
       Scroll down             C-Down or J    C-Down
       Scroll up               C-Up or K      C-Up
       Search again            n              n
       Search backward         ?              C-r
       Search forward          /              C-s
       Start of line           0              C-a
       Transpose chars                        C-t

## Misc

    d  detach
    t  big clock
    ?  list shortcuts
    :  prompt

## Configurations Options

    # Mouse support - set to on if you want to use the mouse
    * setw -g mode-mouse off
    * set -g mouse-select-pane off
    * set -g mouse-resize-pane off
    * set -g mouse-select-window off

    # Set the default terminal mode to 256color mode
    set -g default-terminal "screen-256color"

    # enable activity alerts
    setw -g monitor-activity on
    set -g visual-activity on

    # Center the window list
    set -g status-justify centre

    # Maximize and restore a pane
    unbind Up bind Up new-window -d -n tmp \; swap-pane -s tmp.1 \; select-window -t tmp
    unbind Down
    bind Down last-window \; swap-pane -s tmp.1 \; kill-window -t tmp

# Use Cases

## Split panes

- Start a tmux session:
    + tmux new-session -s <your_session_name>
- To split vertically:
    + `ctrl-b %`
- To split horizontally:
    + `ctrl-b "`
- To navigate and select a pane:
    + `ctrl-b <arrow keys>`
- To toggle full-screen zoom in/out on the current pane:
    + `ctrl-b z`
- To close the current pane:
    + ctrl-b x then confirm with y or n

## Session management

- Start with a named session:
    - tmux new-session -s <your_session_name>
    - `tmux new -s <name>`
- Do your work in your tmux session
- Detach from your session when you are done:
    - tmux detach
- [Optional] View available attachable sessions:
    - tmux list-sessions or `tmux ls`
- Reattach to your tmux session when you are ready to continue working:
    - tmux attach -t <your_session_name>
    - `tmux a -t <name>`
    - `tmux a #`: last created session

# Tips and Tricks

## Unset an environment variable for the session

- `tmux set-environment -r <ENV_VAR>`

## Nested local and remote tmux sessions

- Built-in way
    + `Ctrl + b` once to execute the `prefix` for the local tmux session
    + `Ctrl + b` twice to send the `prefix` to the remote tmux session
- Others
    + https://www.freecodecamp.org/news/tmux-in-practice-local-and-nested-remote-tmux-sessions-4f7ba5db8795/

## List of colors

```bash
for i in {0..255}; do
    printf "\x1b[38;5;${i}mcolour${i}\x1b[0m\n"
done
```

## Copy and Paste

- https://awhan.wordpress.com/2010/06/20/copy-paste-in-tmux/

