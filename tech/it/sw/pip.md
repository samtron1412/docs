[TOC]

# Overview

# Tips and Tricks

## Restricting pip to work on virtualenv only in macOS

- https://hackercodex.com/guide/python-development-environment-on-mac-osx/
- Create `~/Library/Application\ Support/pip/pip.conf`

```
[install]
require-virtualenv = true

[uninstall]
require-virtualenv = true
```

- Create a global pip function in shell script

```
gpip(){
   PIP_REQUIRE_VIRTUALENV="0" pip3 "$@"
}
```

- Upgrade global packages
    + `gpip install --upgrade pip setuptools wheel virtualenv`
