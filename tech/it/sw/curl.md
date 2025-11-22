[TOC]

# Overview

- curl free online book (RECOMMENDED)
    + https://everything.curl.dev/
- Feature comparison table
    + https://curl.se/docs/comparison-table.html
- Man page
    + https://curl.se/docs/manpage.html
- HTTP scripting
    + https://curl.se/docs/httpscripting.html

# Showing details of all requests

- `curl ... --verbose`
- Example:

```
/usr/bin/curl -X 'POST' \                                                                                                                                                                               <<<
  'https://endpoint.com/profiles/<id>/jobs/<id>' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "jobRunParameters": {
    "datasetDate": "20250705T00:00:00+0000"
  }
}' -L --cookie ~/.test/cookie --cookie-jar ~/.test/cookie --verbose
```

- For each request:
    + Make DNS requests to find the IP address of the domain name.
    + Perform TLS handshake to verify the domain name using the CA
      (certificate authority) file (eg.,
      `/etc/pki/tls/certs/ca-bundle.crt`)
    + Make the HTTP request to the endpoint (with the User-Agent,
      accept, Content-Type, Content-Length, etc.)
    + Receive the response with headers (Set-Cookie, Location, etc.)

# Tips and Tricks

## curlie - Syntactic sugar on top of curl for HTTP and HTTPS requests

- https://github.com/rs/curlie
- `brew isntall curlie`

## Show request header

`curl -I <url>`
