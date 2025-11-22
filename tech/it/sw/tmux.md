[TOC]

# Overview

- Books
    + https://leanpub.com/the-tao-of-tmux/read
- https://github.com/gpakosz/.tmux
- Pair programming: https://github.com/zolrath/wemux/
- Advanced Use
    + https://github.com/tmux/tmux/wiki/Advanced-Use

# Configuration

- User-specific configuration: `~/.tmux.conf`
- Global configuration: `/etc/tmux.conf`

- https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/
- color
    + https://superuser.com/questions/285381/how-does-the-tmux-color-palette-work

## Binding keys (shortcuts)

- `tmux` allows a command to be bound to most keys, with or without a
  prefix key.
    + When specifying keys, most represent themselves (for
  example ‘A’ to ‘Z’).
    + Ctrl keys may be prefixed with ‘C-’ or ‘^’, Shift keys with ‘S-’ and Alt (meta) with ‘M-’.
    + In addition, the following special key names are accepted: `Up,
      Down, Left, Right, BSpace, BTab, DC (Delete), End, Enter, Escape,
      F1 to F12, Home, IC (Insert), NPage/PageDown/PgDn,
      PPage/PageUp/PgUp, Space, and Tab`.
    + Note that to bind the ‘"’ or ‘'’ keys, quotation marks are
      necessary, for example:
        * `bind-key '"' split-window`
        * `bind-key "'" new-window`
- A command bound to the `Any` key will execute for all keys which do
  not have a more specific binding.
- Show current binding keys: `prefix-?`
- `bind -r`
    + With -r, you can press the prefix key once, then repeat the bound
      key multiple times without pressing the prefix again (until the
      repeat period expires).
- Arrow keys binding
    + `bind Up select-pane -U`: `Down`, `Left`, `Right`

# Servers

- `tmux` follows client-server model in which the clients can use a
  socket to connect to a server.
    + For each server, multiple clients can connect to that server using
      a socket. Each server is associated to a socket.
        * The default location of socket is in: `/tmp/tmux-{uid}/`
          folder. The `uid` is the user ID of the current login user of
          the operating system.
        * To get the user ID: `id -u` on Linux.
    + Each server can have multiple sessions.
    + Each session can have multiple windows.
    + Each window can have multiple panes and can be linked to multiple
      sessions.
    + Each pane is linked to a pseudo terminal (`man 4 pty`).
- To create a new `tmux` server, we can use `-L <socket-name>` or `-S
  <socket-path>`
    + https://github.com/tmux/tmux/wiki/Advanced-Use#socket-and-multiple-servers
    + `tmux -L new-server-name`
        * `tmux -L new-server-name <command> ...`
    + `tmux -S /tmp/new-server`

# Clients and Sessions

# Windows and Panes

# Buffers

# Hooks

- `tmux` allows commands to run on various triggers, called hooks.
    + Most tmux commands have an after hook and there are a number of
      hooks not associated with commands.
- Hooks are stored as array options, members of the array are executed
  in order when the hook is triggered.
    + Like options different hooks may be global or belong to a session,
      window or pane.
    + Hooks may be configured with the set-hook or set-option commands
      and displayed with show-hooks or show-options -H.
    + The following two commands are equivalent:

        set-hook -g pane-mode-changed[42] 'set -g status-left-style bg=red'
        set-option -g pane-mode-changed[42] 'set -g status-left-style bg=red'

- Setting a hook without specifying an array index clears the hook and sets the first member of the array.
- A command's after hook is run after it completes, except when the command is run as part of a hook itself.
    + They are named with an ‘after-’ prefix.
    + For example, the following command adds a hook to select the
      even-vertical layout after every split-window:

        set-hook -g after-split-window "selectl even-vertical"

- If a command fails, the ‘command-error’ hook will be fired.  For example, this could be used to write to a log file:

        set-hook -g command-error "run-shell \"echo 'a tmux command failed' >>/tmp/log\""

- All the notifications listed in the CONTROL MODE section are hooks (without any arguments), except %exit.

# Status Line

    Symbol    Meaning
    *         Denotes the current window.
    -         Marks the last window (previously selected).
    #         Window activity is monitored and activity has been detected.
    !         Window bells are monitored and a bell has occurred in the window.
    ~         The window has been silent for the monitor-silence interval.
    M         The window contains the marked pane. (can mark and unmark with prefix-m)
    Z         The window's active pane is zoomed.

# Plugins

## Tmux Plugin Manager (tpm)

- https://github.com/tmux-plugins/tpm
- Installation
    + `git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm`
    + Add the config to `.tmux.conf`
    + Reload the `.tmux.conf`: `prefix + r` / `prefix + :source-file ~/.tmux.conf`
- Install plugins: `prefix + I`

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

    <prefix> :new<CR>  new session
    <prefix> s  list sessions and switch between sessions
    <prefix> $  name session
    <prefix> L  go to the last session

## Windows (tabs)

    <prefix> c  new window
    <prefix> w  list windows
    <prefix> f  find window
    <prefix> ,  name window
    <prefix> &  kill window with confirmation
    <prefix> l  go to the last window

## Panes (splits)

    <prefix> %  vertical split
    <prefix> "  horizontal split

    <prefix> x  kill pane with confirmation
    <prefix> +  break pane into window (e.g. to select text by mouse to copy)
    <prefix> -  restore pane from window
    <prefix> ⍽  space - toggle between layouts
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

- Inside a tmux session:
    + `prefix :set-environment -ug <ENV_VAR>`
- When creating a new session
    + `tmux set-environment -r <ENV_VAR>`

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


# Troubleshooting

## server protocol version mismatch (client x, server y)

- Root cause: Different version between tmux client and server.
- Reason:
    + Usually different version of tmux are on the system, so the server
      is run with one version and the client is another version.
    + Check your `PATH` and find all different versions of tmux using
      `which -a tmux` or `where tmux`.
    + Make sure there is only one version of tmux in your system.
- For example:
    + `ssh dev "tmux attach"`: this will only spawn a non-interactive
      shell, so some of the `PATH` are not configured.
