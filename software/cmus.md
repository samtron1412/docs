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
- `</>`: seek by one minute
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

# Configuration
## Files

## Environment

# References
- [Homepage](https://cmus.github.io)
- [Wiki](https://github.com/cmus/cmus/wiki)
