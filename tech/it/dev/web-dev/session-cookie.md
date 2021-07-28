# Cookie
Small piece of data, store at client side, send to server every page load, have time expire.

# Session
A session is a combination of a server-side file containing all the data you wish to store, and a client-side cookie containing a reference to the server data. Clear after close browser.

Cookie is sent to server with a reference data (unique session id), it is used to retrieve session data in server-side file containing all the data.

# Real use
With flat server-side file cannot solve problem of multi server (load balance), each server have own its session file -> store session data to database can solve this problem.

Combination Cookie and Database to store session, and implement "Remember me"

# Resources
- [PHP cookies and session](http://www.tuxradar.com/practicalphp/10/0/0)
- 