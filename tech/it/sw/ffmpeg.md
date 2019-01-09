[TOC]

# Overview

# Tips and Tricks

## Converting video files to mp3

`for i in video/*; do name=${i##*/}; ffmpeg -i "$i" -b:a 128k -f mp3 mp3/"${name%.*}.mp3"; done`

- `name=${i##*/}`: get the filename with extension
- `${name%.*}`: get the name without the extension

## Manipulating audio channels

# References

[man]: manpage
[audio]: https://trac.ffmpeg.org/wiki/AudioChannelManipulation
