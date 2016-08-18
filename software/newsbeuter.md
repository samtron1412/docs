[TOC]

# Overview
- Newsbeuter is an open-source RSS/Atom feed reader for text terminals.
- It runs on Linux, FreeBSD, Mac OS X and other Unix-like operating systems.
- It was originally written by Andreas Krennmair in 2007 and released under the MIT license.

# Name
- "Newsbeuter" is a pun on the German word "Wildbeuter", which means "hunter-gatherer".

# Usage
- With version <= 2.9, creating `newsbeuter` in `$XDG_CONFIG_HOME` and `$XDG_DATA_HOME` for XDG users.
- Add feed URL in `$XDG_CONFIG_HOME/newsbeuter/urls`
- Configuration in `$XDG_CONFIG_HOME/newsbeuter/config`
- Run: `$ newsbeuter`

# Configuration
```
auto-reload yes
reload-time 15
always-display-description true
browser chromium
download-retries 3
save-path "~/doc/feed"

# podbeuter -------------------------------------------------------------
download-path "~/media/podcast/%h/%n"
max-downloads 4
player mpv


# binding --------------------------------------------------------------
bind-key k up
bind-key j down
bind-key g home
bind-key G end
bind-key J pagedown
bind-key K pageup
```

# References
1. [Arch Wiki - Newsbeuter][1]
2. [Homepage][2]
3. [Documentation][3]

[1]: https://wiki.archlinux.org/index.php/Newsbeuter "Arch Wiki - Newsbeuter"
[2]: http://newsbeuter.org/ "Homepage"
[3]: https://newsbeuter.org/doc/newsbeuter.html "Documentation"
