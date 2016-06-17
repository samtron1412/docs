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

