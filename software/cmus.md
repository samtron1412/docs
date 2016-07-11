[TOC]

# Overview
**cmus (C* MUSic player)** is a small, fast and powerful console audio player which supports most major audio formats.

- `man cmus-tutorial`
- `man cmus`
- `man cmus-remote`: controlling playback through an external application or key-binding.

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

# References
- [Homepage](https://cmus.github.io)
- [Wiki](https://github.com/cmus/cmus/wiki)
