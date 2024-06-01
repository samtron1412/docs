[TOC]

# Overview

Proxy server is a server that acts as an intermediary for request from
clients seeking resources from other servers.

# Types

## Open proxy

Internet -> Open Proxy -> Internet

## Reverse proxy

Internet -> Reverse Proxy -> Internal Web server

+ Forward Proxy (or Proxy) vs. Reverse Proxy
    * Forward Proxy: Acting on behalf of a requestor (or service consumer)
        - `(X <--> Y) <--> Z`
            + X: client, Y: forward proxy, Z: server
        - Sit in front of clients to hide clients from servers.
        - Why?
            + Protect clients' only identities
            + Bypass firewall/restrictions
            + Block access to certain content
    * Reverse Proxy: Acting on behalf of service/content producer.
        - `X <--> (Y <--> Z)`
            + X: client, Y: reverse proxy, Z: server
        - Sit in front of servers to hide servers from clients.
        - In real-file, a system can have multiple layers of reverse
          proxies: edge servers (CDN), API Gateway/load balancers
        - Why?
            + Protect servers
            + Load balancing
            + Caching to improve performance
            + Handles SSL encryption/termination
    * https://stackoverflow.com/questions/224664/whats-the-difference-between-a-proxy-server-and-a-reverse-proxy-server
    * https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy
