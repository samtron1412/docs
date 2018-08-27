[TOC]

# Overview

Mac OS

# Tuning Mac

- https://github.com/nikitavoloboev/my-mac-os
- https://github.com/serhii-londar/open-source-mac-os-apps
- https://github.com/iCHAIT/awesome-macOS
- https://github.com/jaywcjlove/awesome-mac

# Tips and Tricks

## Key repeat

- Hold a key and it will repeat the key in Sublime Text in vim mode
- https://gist.github.com/conficker1805/18830beb333a990b22a3

```
You can disable this feature for just Sublime Text by issuing the
following command in your terminal (not the Sublime Text console):

defaults write com.sublimetext.3 ApplePressAndHoldEnabled -bool false

Note: replace com.sublimetext.3 with whichever version of Sublime Text
you are running eg. 'com.sublimetext.2'

Alternately, if you want this feature disabled globally, you can enter
this:

defaults write -g ApplePressAndHoldEnabled -bool false

In either case you'll need to restart Sublime Text for the change to
take place.
```

## Create a Python development environment

- https://www.digitalocean.com/community/tutorials/how-to-install-python-3-and-set-up-a-local-programming-environment-on-macos
- https://hackercodex.com/guide/python-development-environment-on-mac-osx/
- install homebrew
- install python through brew install python
- install virtualenv through pip install virtualenv
