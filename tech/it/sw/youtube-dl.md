[TOC]

# Overview

`youtube-dl -F <link>`: list all available formats of requested videos

- `youtube-dl -f <format> <link>`: Download the video format code.
    + `<link>` can be a playlist
    + `<format>`: mp4, webm, mkv
    + `youtube-dl -f mp4 https://www.youtube.com/playlist?list=PLSJl4Xusm04tbstMd4rSqsFQsP4vIdY7k`

# Alternatives

## you-get

- https://you-get.org/
- https://github.com/soimort/you-get

## yt-dlp

- https://github.com/yt-dlp/yt-dlp
- A fork from `youtube-dl` with additional features

# Tips and Tricks

## Download mp3

- `youtube-dl --extract-audio --audio-format mp3 <video URL>`
- `youtube-dl --extract-audio --audio-format mp3 --playlist-items 5-10 youtube-playlist-url`

