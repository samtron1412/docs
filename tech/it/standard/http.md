[TOC]

# Overview


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