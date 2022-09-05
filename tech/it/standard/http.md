[TOC]

# Overview

- https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview
- HTTP is a protocol for fetching resources such as HTML documents.
- HTTP/1.1 (1997)
    + HTTP verbs for requests
    + Reuse a single TCP connection
- HTTP/2 (2015)
    + Multiplexing many concurrent requests/responses through a single
      TCP/IP connection
- HTTP/3 (2022)
    + Use QUIC + UDP instead of TCP
- View protocol versions in DevTool of each browser
    + Chrome: Network -> Protocol (column, right click to choose)
- How does browser know which version of HTTP to use?
    + https://superuser.com/questions/1659248/how-does-browser-know-which-version-of-http-it-should-use-when-sending-a-request


# [Status code](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)

## 301 Moved Permanently

First Time Around:

1.1: User enters link to site A, or clicks on a link directed at Site A
1.2: Browser interprets link at Site A, first time, no cache. Sends GET to Site A.
1.2: Site A responds with 301 Redirect to Site B
1.3: Browser sends GET to Site B.

Any Subsequent Times Around:

2.2: User clicks on a link directed at Site A
2.2: Browser sees that, due to a past 301 redirect, Site A should now be Site B.
2.3: Without initiating any request whatsoever at Site A, browser initiates GET at Site B.
