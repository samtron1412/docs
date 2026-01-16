[TOC]

# Overview

- https://web.dev/howbrowserswork/
- A web browser (commonly referred to as a browser) is a software
  application for retrieving, presenting, and traversing information
  resources on the World Wide Web.

# Browser Engines

- https://en.wikipedia.org/wiki/Comparison_of_browser_engines
- Popular engines
    + Blink: Chromium-based browsers
    + Gecko: Firefox
    + WebKit: Apple ecosystem
    + Trident: Windows

# Browser / Web storage

- https://en.wikipedia.org/wiki/Web_storage
- https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Client-side_storage
- Cookies
    + Specification:
        * https://datatracker.ietf.org/doc/html/rfc6265
    + https://en.wikipedia.org/wiki/HTTP_cookie
    + https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
    + Shared storage between client and server.
    + Automatically send with the HTTP requests to servers.
    + Persistent until expiration or explicitly delete.
    + Most common for authentication and authorization.
        * Secure with flags: `HttpOnly` (only server can read),
          `SameSite` to prevent CSRF (Cross-Site Request Forgery) attack.
    + Limit: 4KB, string only.
- Local storage
    + https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API
    + Stores data with no expiration date, and gets cleared only through
      JavaScript, or clearing the Browser cache / Locally Stored Data.
    + Data is never transferred to the server.
    + Only support string data structure.
- Session storage
    + https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API
    + Stores data only for a session, meaning that the data is stored
      until the browser (or tab) is closed.
        * Refresh/reload tabs does not clear this data.
    + Data is never transferred to the server.
    + Storage limit is larger than a cookie (at most 5MB as of 2023).
    + Only support string data structure.
- IndexedDB
    + https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API
    + Support many structured data including files/blobs.
    + Use indexes to enable high-performance searches of data.
    + IndexedDB is a transactional database system, like an SQL-based
      RDBMS. However, unlike SQL-based RDBMSes, which use fixed-column
      tables, IndexedDB is a JavaScript-based object-oriented
      database. IndexedDB lets you store and retrieve objects that are
      indexed with a key; any objects supported by the structured clone
      algorithm can be stored. You need to specify the database schema,
      open a connection to your database, and then retrieve and update
      data within a series of transactions.
- Cache storage
    + https://developer.mozilla.org/en-US/docs/Web/API/Cache
    + Storing HTTP responses to specific requests.
    + Useful to store website assets offline.


| Topic               | Cookies           | Session Storage    | Local Storage                |
|---------------------|-------------------|--------------------|------------------------------|
| Storage capacity    | 4KB               | 5MB                | 5/10 MB depending on browser |
| expiration          | manually set      | when close the tab | never expires                |
| can be accessed on  | client and server | client only        | client only                  |
| sent with request   | yest              | no                 | no                           |
| supported data type | string            | string             | string                       |
| editable by users   | yes               | yes                | yes                          |


