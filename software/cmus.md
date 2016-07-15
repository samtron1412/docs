[TOC]

# Overview
**cmus (C* MUSic player)** is a small, fast and powerful console audio player which supports most major audio formats.

- `man cmus-tutorial`
- `man cmus`
- `man cmus-remote`: controlling playback through an external application or key-binding.

# User Interface
## Views
There are 7 views in cmus. Press keys 1-7 to change active view.
- **Library view (1)**: Display all tracks. Tracks are sorted artist/album tree. Artist sorting is done alphabetically. Albums are sorted by year.
- **Sorted library view (2)**: Displays same content as view 1, but as a simple list which is automatically sorted by user criteria.
- **Playlist view (3)**: Displays editable playlist with optional sorting.
- **Play Queue view (4)**: displays queue of tracks which are played next. These tracks are played before anything else.
- **Browser (5)**: Directory browser. In this view, music can be added to either the library, playlist or queue from the filesystem.
- **Filter view (6)**: Lists user defined filters.
- **Settings view (7)**: Lists keybinding, unbound commands and options. Remove bindings with `d` or `del`, change bindings and variables with `enter` and toggle variables with `space`.

## Status line

## Command line


# Tutorials
## Adding music
- Press `5` to switch to the file-browser view.
- Using the arrow keys, Enter and Backspace to navigate to where you have audio files stored.
- Press `a` to add music (file/folder).

## Playing music
- `c`: pause/unpause
- `right/left arrow`: seek by 10 seconds
- `,/.`: seek by one minute
- Options to control what plays next when the track ends. The state of these settings are shown in the bottom right corner.
	+ The first shows what collection of tracks we are playing. Press `m` to cycle through the different options
		* `all from library`
		* `artist from library`
		* `album from library`
	+ To the right of the first part is the state of three toggles.
		* `[C]ontinue`: When this is off, cmus will always stop at the end of the track. You can toggle this by pressing `shift-c`
		* `[R]epeat`: If this is on (and continue is on), when cmus reaches the end of the group of tracks you're playing (selected with the `m` key) it will start again from the beginning. Press `r` to toggle this setting.
		* `[S]huffle`: When this is on, cmus will choose a random order to play all the tracks once. Press `s` to toggle this option.

## The Queue
- You're listening to a song, and you want to select which song will play next, without interrupting the currently playing song.
	+ Go to the song you want to hear next (in any of the views)
	+ Press `e`
- The queue is not affected by the "shuffle" option.
- Press `4` to view/edit the queue.
	+ Change the order of the tracks with the `p` and `P` keys.
	+ Remove a track `shift-d`.
- When cmus is ready to play another track (it's reached the end of a track and the "continue" setting is on) it will remove the top entry from the queue and start playing it.

## The playlist
- The playlist works like another library (like view `2`) except that you manually set the order of the tracks (like the queue).
- Add some tracks:
	+ Press `2` to go to the library view
	+ Press `y` to add a track to the playlist.
- Edit playlist: using `p, P, D` to move and delete tracks.
- To put cmus into "play from the playlist" mode, press Enter on one of the tracks in the playlist. To switch modes without interrupting the currently-playing song, press `shift-m`.


## Filter
Filters are used mostly for filtering contents of library views (1 and 2). Filters do not change the actual library content, i.e. `:save` command will still save all tracks to playlist file whether they are visible or not.

### Types
There are three types of filter expressions, each offering more expressiveness:
- simple: `beatles`
- short: `~a beatles (!~y1960-1965 | ~d>600)`
- long: `artist="*beatles*"&album="R*"`

Simple expressions are only available using live-filter. For other filter commands the type is auto-detected, so both short and long expressions can be used.

Long expressions are list of built-in filters or user defined filters separated with `&` or `|`. Parenthesis can be used group subexpressions and `!` negates result of the expression following it. Same is true for short expressions, but they can only be made of built-in filters.

### Strings
- long: filename, artist, albumartist, album, title, genre, comment, codec, codec_profile, media.
	+ Comparators: `=` and `!=`
- short: ~f, ~a, ~A, ~l, ~t, ~g, ~c

### Integers
- long: discnumber, tracknumber, date(year), originaldate (year), duration (seconds), bitrate
	+ Comparators: `<`, `<=`, `=`, `>=`, `>`, `!=`
- short: ~D, ~n, ~y, ~d
	+ Comparators: `<`, `>`
	+ Ranges: `a-b` (a<=x<=b), `-b` (<=b), `a-`(>=a)

### Booleans
- `tag` (true if track has tags). `~T`
- `stream` (true if track is a stream). `~s`

### Defining filters
- `:fset ogg=filename="*.ogg"`
- Using user defined filter `ogg`: `:fset 90s-ogg-mp3=date>=1990&date<2000&(ogg|filename="*.mp3")`

### Activating filters
- `:factivate ogg`
- `:factivate !ogg`
- Or select the filters by pressing `space` in view 6 and then activate by pressing `enter`.

### Throw-away filters
- `:filter date>=1980&genre="*rock*"`: unactivates all filters in the filters view and apply this one.
- `:live-filter`: apply in addition to all currently activated filters.

### Selecting tracks matching a filter
- `:mark duration<120`
- `:mark play_count>=1`

# Configuration
## Files
cmus reads its configuration from 3 different places
- `$XDG_CONFIG_HOME/cmus/autosave`: this is the first file cmus loads. cmus saves its state on exit to this file so you shouldn't edit it.
- `/usr/share/cmus/rc`: If the autosave file didn't exist, this file is read instead.
- `$XDG_CONFIG_HOME/cmus/rc`: Static config file. This file is read immediately after the autosave file, and is never modified by cmus. You can override auto-saved setting in this file.

Color Scheme: `colorschem zenburn`

## Key binding

# Tips and Tricks
## Shell scripts
The shell scripts to be executed via `:shell` command. Usually they use `cmus-remote` to get information from cmus and execute commands/modify variables.

**cmus-edit-tags**

```shell
#!/bin/sh
file=$(/usr/bin/cmus-remote -C 'echo {}')

if [ -f "$file" ]
then /usr/bin/puddletag "$file"
else /usr/bin/cmus-remote -C "echo Oops, couldn't file selected tracks"
fi
```

Execute the script by: `:shell cmus-edit-tags` or binding a key: `bind -f common 0 shell ~/bin/cmus-edit-tags`


# References
- [Homepage](https://cmus.github.io)
- [Wiki](https://github.com/cmus/cmus/wiki)
