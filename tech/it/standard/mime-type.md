[TOC]

# Overview

A media type (also MIME type and content type) is a two-part identifier
for file formats and format contents transmitted on the Internet.

The [Internet Assigned Numbers Authority (IANA)][iana] is the official
authority for the standardization and publication of these
classifications.

Media types were first defined in [RFC 2045][2045]

# Naming

A media type is composed of a type, a subtype, and optional parameters.

As an example, an HTML file might be designated `text/html;
charset=UTF-8`.
- `text` is the type
- `html` is the subtype
- `charset=UTF-8` is an optional parameter indicating the character
  encoding.

Media type consists of top-level type name and sub-type name, which is
further structured into so-called "trees".
- `<top-level type name>/<sub-type name><[; parameters]>`
- `<top-level type name>/<[tree.]> <sub-type name> <[+suffix]><[; parameters]>`

Top-level type names: `application`, `audio`, `example`, `image`,
`message`, `model`, `multipart`, `text`, `video`, `chemical`.

| Top-level type   | Description                                                | Sub-type                                                                                                                                    |
| -                | -                                                          | -                                                                                                                                           |
| application      | Files with binary content: documents, archives,...         | epub+zip, ereader, excel, gbr, gzip                                                                                                         |
| audio            | audio files                                                | flac, m4a, midi                                                                                                                             |
| chemical         | Chemical information, molecular and other chemical data    | x-cif, x-cml, x-daylight-smiles, x-gamess-input, x-gaussian-checkpoint                                                                      |
| image            | Image files                                                | bmp, crw, g3fax, gif, jpeg, jpg                                                                                                             |
| inode            | Can be opened by a file manager                            | blockdevice, chardevice, directory, fifo, mount-point, socket, symlink                                                                      |
| message          | Message protocols                                          | delivery-status, disposition-notification, external-body, news, partial, frc822, x-gnu-rmail                                                |
| misc             | Streaming meta data                                        | ultravox                                                                                                                                    |
| text             | Text documents                                             | html, javascript, mathml, mml, plain                                                                                                        |
| video            | Video  files                                               | flv, mp2t, mp4                                                                                                                              |
| x-content        | Content on disks such as audio, video, image or blank disk | audio-cdda, audio-player, blank-bd, blank-cd, blank-dvd, blank-hddvd, image-picturecd, video-dvd, video-svcd                                |
| x-scheme-handler | Internet protocol                                          | ftp, geo, ghelp, help, http, https, icy, icyx, info, irc, magnet, mailto, man, mms, mmsh, net, pnm, rtmp, rtp, rtsp, skype, uvox, vnc, xmpp |
| x-epoc           | SISX package                                               | x-sisx-app                                                                                                                                  |
| multipart        | Multi-part mime messages                                   | alternative, appledouble, digest, encrypted, mixed, related, report, signed, x-mixed-replace                                                |
| model            | such as 3D model                                           | x-kpovmodeler, vrml, x-modelica                                                                                                             |

# Mailcap

Mailcap (derived from the phrase `mail capability`) is a type of meta
file used to configure how MIME-aware applications such as mail clients
and web browsers render files of different MIME-types.

The mailcap format is defined by [RFC 1524][1524] but is not defined as
an Internet standard.

Lines can be comments starting with the `#`character, or a mime-type
followed by how to handle that mime type. The first part is called the
content-type, and the second part is called the view-command.
- `video/mpeg; xmpeg %s`: says if a file encoded in mime has type
  video/mpeg, run the xmpeg program with the file name as a parameter.

# mime.types

An associated file is the `mime.types` file, which associates filename
extensions with a MIME type.

If the MIME type is properly set, this is unnecessary, but MIME types
may be incorrectly set, or set to a generic type such as `application
/octet-stream`, and `mime.types` allows one to fall back on the
extension in these cases.

When viewing a file, these two work together as follows: `mime.types`
associates an extension with a MIME type, while `mailcap` associates a
MIME type with a program.

In UNIX-like systems, the mime.types file is usually located at
`/etc/mime.types` and/or `~/.mime.types` and the format is simply that
each line is a space-delimited list of a MIME type, followed by zero or
more extensions.
- `text/html htm html`

# References

[wiki]: https://en.wikipedia.org/wiki/Media_type
[awiki]: https://wiki.archlinux.org/index.php/Default_applications
[spec]: https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html
[database]: https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176
[iana]: https://en.wikipedia.org/wiki/Internet_Assigned_Numbers_Authority
[2045]: https://www.ietf.org/rfc/rfc2045.txt
[1524]: https://tools.ietf.org/html/rfc1524
