[TOC]

# Overview

There is frequently more than one application able to handle data of a
certain type, so users and even some packages assemble lists of default
application for each MIME type.
- Some desktop environments will define default applications.

# MIME types

Before setting the default application per file type, the file type must
be detected. There are two common ways to do that:

1. Using the file name extension (e.g. `.html`)
2. Using a [magic number][magic-num] in the first few bytes of the file.

However, it is possible that a single file type is identified by several
different magic numbers and file name extensions, so [MIME types][wiki]
are used to represent distinct file types.

MIME database can be used by other packages to register new MIME types.

## MIME database

The system maintains a database of recognized MIME types: the [shared
MIME-info database][database]
- The database is built from the XML files installed by packages in
`/use/share/mime/packages` using the tools from the [shared-mime-info]
[shared-mime-info] package.
- The files in `/usr/share/mime/` should not be directly edited. You
should maintain a separate database on a per-user basis in the
`~/.local/share/mime/` tree.

### New MIME types

This example defines a new MIME type `application/x-foobar` and assigns
it to any file with a name ending in `.foo`.

Create the following file:
`~/local/share/mime/packages/application-x-foobar.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mime-info xmlns="http://www.freedesktop.org/standards/shared-mime-info">
    <mime-type type="application/x-foobar">
        <comment>foo file</comment>
        <icon name="application-x-foobar"/>
        <glob-deleteall/>
        <glob pattern="*.foo"/>
    </mime-type>
</mime-info>
```

And then update the MIME database:
`$ update-mime-database ~/.local/share/mime`

>You have to create new desktop entries or modify `mimeapps.list` and
associate with this new MIME type.

## Desktop entries

Each package can use desktop entries to provide information about the
MIME types that can be handled by the software.
- `/usr/share/applications/mimeinfo.cache` is the only file that
programs need to read to find all desktop files that might be used to
handle given MIME type.
- The files in `/usr/share/applications/` should not be edited directly.
You should maintain a separate database on a per-user basis in the
`~/.local/share/applications/` tree.

# Set default applications

The configuration of default applications depends on which launcher is
used. Unfortunately there are multiple incompatible standards and many
programs even have their own custom formats.

The most common standards for manual editing are:
- Environment variables
- XDG standard
- mailcap

You can also use some utility to do the job.

## Environment variables

Console programs in particular are configured by setting an appropriate
environment variable, e.g. `BROWSER` or `EDITOR`

## XDG standard

The [XDG standard][xdg-standard] is the most common for configuring
desktop environments.
- Default applications for each MIME type are stored in `mimeapps.list`
files, which can be stored in several locations. They are searched in
the following order:

| Path                                    | Usage                          |
| -                                       | -                              |
| `~/.config/mimeapps.list`               | user overrides                 |
| `/etc/xdg/mimeapps.list`                | system-wide overrides          |
| `/usr/share/applications/mimeapps.list` | distribution-provided defaults |

## mailcap

The `mailcap` file formats is used by mail programs such as `mutt` to
open non-text files. To have those programs use `xdg-open`, edit
`~/.mailcap`

`*/*; xdg-open "%s"`

# Utilities

## xdg-utils

```bash
# determine a file's MIME type
$ xdg-mime query filetype photo.jpeg
image/jpeg

# determine the default application for a MIME type
$ xdg-mime query default image/jpeg
gimp.desktop

# change the default application for a MIME type
$ xdg-mime default feh.desktop image/jpeg

# open a file with its default application
$ xdg-open photo.jpeg

# shortcut to open all web MIME types with a single application
$ xdg-settings set default-web-browser firefox.desktop

# shortcut for setting the default application for a URL scheme
$ xdg-settings set default-url-scheme-handler irc xchat.desktop
```

>If no desktop environment is detected, MIME type detection falls back
to using `file` which, ironically, does not implement the XDG standard.
If you want `xdg-utils` to work properly without a desktop environment,
you will need to install `perl-file-mimeinfo` or another alternatives.

## xdg-open alternatives

Because of the complexity of the xdg-utils version of `xdg-open`, it can
be difficult to debug when the wrong default application is being
opened.
- There are many alternatives that attempt to improve upon it.
- Several of these alternatives replace the `/usr/bin/xdg-open` binary

### perl-file-mimeinfo

perl-file-mimeinfo provides the tools `mimeopen` and `mimetype`. These
have a slightly nicer interface than xdg-utils equivalents.

>Most importantly, `xdg-utils` apps will actually call `mimetype`
instead of `file` for MIME type detection, if possible.

## lsdesktopf

# Troubleshooting

# References

[awiki]: https://wiki.archlinux.org/index.php/Default_applications
[magic-num]: https://en.wikipedia.org/wiki/List_of_file_signatures
[wiki]: https://en.wikipedia.org/wiki/MIME_type
[database]: https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176
[shared-mime-info]: https://www.archlinux.org/packages/?name=shared-mime-info
[xdg-standard]: https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html
