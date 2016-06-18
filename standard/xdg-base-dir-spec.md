[TOC]

# Overview
**XDG Base Directory Specification**: Various specifications specify files and file formats. This specification defines where these files should be looked for by defining one or more base directories relative to which files should be located.

# Basics
- User-specific data files: `$XDG_DATA_HOME`
- User-specific configuration files: `$XDG_CONFIG_HOME`
- Set of preference ordered base directories relative to which data files should be searched: `$XDG_DATA_DIRS`
- Set of preference ordered base directories relative to which configuration files should be searched: `$XDG_CONFIG_DIRS`
- User-specific non-essential (cached) data: `$XDG_CACHE_HOME`
- User-specific runtime files and other file objects: `$XDG_RUNTIME_DIR`

All paths set in these environment variables must be absolute.

# Environment variables
- `$XDG_DATA_HOME`: default `$HOME/.local/share`
- `$XDG_CONFIG_HOME`: default `$HOME/.config`
- `$XDG_DATA_DIRS`: default `/usr/local/share/:/usr/share/`
- `$XDG_CONFIG_DIRS`: default `/etc/xdg`
- `$XDG_CACHE_HOME`: default `$HOME/.cache`
- `$XDG_RUNTIME_DIR`: init system
