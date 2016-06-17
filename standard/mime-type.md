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

Top-level type names: `application`, `audio`, `example`, `image`, `message`, `model`, `multipart`, `text`, `video`.

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
