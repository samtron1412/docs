[TOC]

# Overview

The freedesktop.org [Desktop Entry specification][desktop-spec] provides
a standard for applications to integrate into a desktop environment.

**Desktop entries** are the configuration files that describe how an
application is launched and which data it can handle. They also
configure how an application appears in a menu with an icon, which is
subject to the related [menu specification][menu-spec] standard.

The most common desktop entries are the `.desktop` and `.directory`
files.

There are roughly three types of desktop entries:
- **Application**: a shortcut to an application
- **Link**: a shortcut to a web link
- **Directory**: a container of meta data of a menu entry

# Application entry

Desktop entries for application, or `.desktop` files, are generally a
combination of meta information resources and a shortcut of an
application.
- System-wide: `/usr/share/applications` or
`/usr/local/share/applications`
- User-specific: `~/.local/share/applications`

## File example

The complete list of keys can be found in the [freedesktop.org
specification][desktop-spec]

```
[Desktop Entry]

# The type as listed above
Type=Application

# The version of the desktop entry specification to which this file complies
Version=1.0

# The name of the application
Name=jMemorize

# A comment which can/will be used as a tooltip
Comment=Flash card based learning tool

# The path to the folder in which the executable is run
Path=/opt/jmemorise

# The executable of the application, possibly with arguments.
Exec=jmemorize

# The name of the icon that will be used to display this entry
Icon=jmemorize

# Describes whether this application needs to be run in a terminal or not
Terminal=false

# Describes the categories in which this entry should be shown
Categories=Education;Languages;Java;
```

# Icons

See also the [Icon Theme Specification][icon-spec]

## Common image formats

| Extension | Full Name                   | Graphics Type | Container Format | Supported |
| -         | -                           | -             | -                | -         |
| .png      | Portable Network Graphics   | Raster        | No               | Yes       |
| .svg      | Scalable Vector Graphics    | Vector        | No               | Yes       |
| .gif      | Graphics Interchange Format | Raster        | No               | No        |
| .ico      | MS Windows Icon Format      | Raster        | Yes              | No        |
| .icns     | Apple Icon Image            | Raster        | Yes              | No          |

## Converting icons

Using the `convert` tool (which is part of the `imagemagick` package)

If you want to know the size of the image, or the number of images in a
container file like `ico` you can use the `identify` tool (also part of
the `imagemagick` package)

# Tools

## gendesk

## lsdesktopf (aur)

Listing available `.desktop` files or searching in their content.

## fbrokendesktop (aur)

Detecting broken `Exec` in a `.desktop` file.

# Tips and tricks

## Hide desktop entries

`NoDisplay=true`

## Modify environment variables

`Exec=env LANG=en_US abiword %U`

# References

[awiki]: https://wiki.archlinux.org/index.php/Desktop_entries
[desktop-spec]: https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html
[menu-spec]: https://specifications.freedesktop.org/menu-spec/menu-spec-latest.html
[icon-spec]: https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html
