[TOC]

# Overview

Mac OS

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
