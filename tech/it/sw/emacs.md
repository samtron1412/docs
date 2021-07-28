[TOC]

# Overview

- Potential features
    + Text editor: coding, note taking (org-mode), markdown, git, latex
    + Email client: m4u
    + File manager: dired (built-in), ranger, sunrise-commander
    + Music player
    + PDF reader
    + Project management
    + IRC, Chat, RSS
    + DevOps

```
first step - run the built-in Emacs tutorial - C-h t
second step - watch the excellent screencast Meet Emacs
third step - visit Mastering Emacs
forth step - read the official Emacs Manual - C-h r
fifth step - use Emacs day and night for all your work
```

## Resources

- Emacs help system

## Installation

- MacOS
    + `brew install --cask emacs`: will install the  GUI version
    + To execute the TUI version: `emacs -nw`

# Running Emacs as a Daemon

- `emacs --daemon`
- `emacsclient -nw`: create a new TUI buffer
- `emacsclient -c`: create a new GUI buffer

# Org mode

- https://www.youtube.com/watch?v=oJTwQvgfgMM

# Emacs for Vim Users

- Spacemacs vs. Doom vs. Vanilla Emacs
    + https://yiming.dev/blog/2018/01/22/compare-doom-emacs-spacemacs-vanilla-emacs/
- https://github.com/syl20bnr/spacemacs
- https://github.com/hlissner/doom-emacs
- https://github.com/emacs-evil/evil
- https://www.emacswiki.org/emacs/Evil

# Tips and Tricks

## GUI vs. TUI

- https://www.reddit.com/r/emacs/comments/4nwvex/gui_vs_terminal_version_of_emacs_recommendations/
- https://superuser.com/questions/193308/emacs-what-features-or-benefits-are-unique-to-either-gui-or-terminal-interface
- https://www.reddit.com/r/emacs/comments/5lh1fg/any_glaringly_large_disadvantages_to_emacs_in_nw/
- GUI:
    + Provide more options for binding keys (some keys can't bind in
      TUI)
    + Colors, fonts, images, etc.
- TUI
    + Good for SSH remotely through tmux/screen
    + Faster
- Can achieve both by running Emacs as a daemon

# References
1. [Wikipedia - Emacs][1]
2. [Arch Wiki - Emacs][2]
3. [Wikipedia - Gnus][3]
4. [Documentation][4]

[1]: https://en.wikipedia.org/wiki/Emacs "Wikipedia - Emacs"
[2]: https://wiki.archlinux.org/index.php/Emacs "Arch Wiki - Emacs"
[3]: https://en.wikipedia.org/wiki/Gnus "Wikipedia - Gnus"
[4]: https://www.gnu.org/software/emacs/documentation.html "Documentation"
