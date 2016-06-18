[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/Media_type)
- [Arch Wiki](https://wiki.archlinux.org/index.php/Default_applications)

A media type (also MIME type and content type) is a two-part identifier for file formats and format contents transmitted on the Internet.

The [Internet Assigned Numbers Authority (IANA)](https://en.wikipedia.org/wiki/Internet_Assigned_Numbers_Authority) is the official authority for the standardization and publication of these classifications.

Media types were first defined in [RFC 2045](https://www.ietf.org/rfc/rfc2045.txt)

# Naming
A media type is composed of a type, a subtype, and optional parameters.

As an example, an HTML file might be designated `text/html; charset=UTF-8`.
- `text` is the type
- `html` is the subtype
- `charset=UTF-8` is an optional parameter indicating the character encoding.

Media type consists of top-level type name and sub-type name, which is further structured into so-called "trees".
- `<top-level type name>/<sub-type name><[; parameters]>`
- `<top-level type name>/<[tree.]> <sub-type name> <[+suffix]><[; parameters]>`

Top-level type names: `application`, `audio`, `example`, `image`, `message`, `model`, `multipart`, `text`, `video`, `chemical`.

# Mailcap
Mailcap (derived from the phrase `mail capability`) is a type of meta file used to configure how MIME-aware applications such as mail clients and web browsers render files of different MIME-types.

The mailcap format is defined by [RFC1524](https://tools.ietf.org/html/rfc1524) but is not defined as an Internet standard.

Lines can be comments starting with the `#`character, or a mime-type followed by how to handle that mime type. The first part is called the content-type, and the second part is called the view-command.
- `video/mpeg; xmpeg %s`: says if a file encoded in mime has type video/mpeg, run the xmpeg program with the file name as a parameter.

# mime.types
An associated file is the `mime.types` file, which associates filename extensions with a MIME type.

If the MIME type is properly set, this is unnecessary, but MIME types may be incorrectly set, or set to a generic type such as `application/octet-stream`, and `mime.types` allows one to fall back on the extension in these cases.

When viewing a file, these two work together as follows: `mime.types` associates an extension with a MIME type, while `mailcap` associates a MIME type with a program.

In UNIX-like systems, the mime.types file is usually located at `/etc/mime.types` and/or `~/.mime.types` and the format is simply that each line is a space-delimited list of a MIME type, followed by zero or more extensions.
- `text/html htm html`

# Default applications
Setting default applications per file type involves detection of the file type as the first step.

Since the application launcher cannot fully understand all file types, the detection is based on reading only a small part of the file.

There are two common ways to determine the file type:
- Using the file name extension, for example `.html` or `.jpeg`
- Using the so-called "magic bytes" at the start of the file.

The first method is very simple and fast, but inaccurate if the file is not named "correctly". The second is more accurate, but slower.

Since files are not required to have an extension and multiple file name extensions can be used for the same file type, MIME types are commonly used instead to uniquely represent the type of a file.

## Archlinux
In Arch, tools from the [shared-mime-info](https://www.archlinux.org/packages/?name=shared-mime-info) package are used to maintain the MIME type database, which is used by other packages to register new MIME types.

Each package can also use the [Desktop entries](https://wiki.archlinux.org/index.php/Desktop_entries) to provide information about the MIME types that can be handled by the packaged software.

There is frequently more than one application able to handle data of a certain MIME type, so users and even some packages assemble lists of default applications for each MIME type.
