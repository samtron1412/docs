[TOC]

# Overview

- Chromium is the open-source web browser project from which google
  Chrome draws its source code.
- Google's intention, as expressed in the developer documentation, was
  that Chromium would be the name of the open-source project and that
  the final product name would be Chrome.
- One of the major aims of the project is for Chromium to be a tabbed
  window manager, or shell for the web, as opposed to it being a
  traditional browser application.
- The application is designed to have a minimalist user interface.

# Tips and Tricks

- https://wiki.archlinux.org/index.php/Chromium/Tips_and_tricks

## Copy curl commands for files under `Network` tab in Developer Tools

- Open developer tools.
- Go to Network tab.
- Right click on the file and select `Copy`, then `Copy as cURL`

## Delete all saved links in OneTab extension

```javascript
// execute the following code in JavaScript console
function delete_single() {
  for (clickable of clickables) {
    if (!clickable || clickable.innerHTML !== "Delete all")
      continue;
    clickable.click();
    return true;
  }
  return false;
}
window.confirm = function() { return true; }
var clickables = document.getElementsByClassName("clickable");
document.addEventListener('DOMNodeRemoved', delete_single, false);
delete_single();
```

## Listen to YouTube playlist non-stop

- https://medium.com/@katopz/how-to-prevent-youtube-from-randomly-pausing-video-da93f1af8cbe
- Copy the JavaScript code and run it in the JS console

# References

1. [Wikipedia - Chromium][1]
2. [Wikipedia - Google Native Client][2]

[1]: https://en.wikipedia.org/wiki/Chromium_(web_browser) "Wikipedia - Chromium"
[2]: https://en.wikipedia.org/wiki/Google_Native_Client "Wikipedia - Google Native Client"
