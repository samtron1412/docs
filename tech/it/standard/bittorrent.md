# Overview

- https://en.wikipedia.org/wiki/BitTorrent
- https://www.bittorrent.org/
    + https://www.bittorrent.org/beps/bep_0003.html
- BitTorrent is a communication protocol for peer-to-peer file sharing
  (P2P), which enables users to distribute data and files over the
  Internet in a decentralized manner.
- Actors:
    + BitTorrent clients: programs that implement BitTorrent protocol.
    + BitTorrent trackers: provide a list of files available for
      transfer and allow the client to find peer users, known as
      "seeds", who may transfer the files.
        * Private trackers require invitation to join, and there are
          rules to follow.
    + Torrent files: metadata files

# Protocol

- Client
    + Download
    + Upload
        * Pick the most givers to upload / give back and ignore takers.

# Torrent files

- https://en.wikipedia.org/wiki/Torrent_file
- A torrent file contains a list of files and integrity metadata about
  all the pieces, and optionally contains a large list of trackers.

# Magnet links

- https://en.wikipedia.org/wiki/Magnet_URI_scheme
- Magnet is a URI scheme that defines the format of magnet links, a de
  facto standard for identifying files (URN) by their content, via
  cryptographic hash value rather than by their location.
- Differences between magnet links and torrent file

```
When you download a torrent file directly, you are getting that .torrent
file from the web server.

When you use a magnet link, the URL you clicked on is passed over to
your torrent client, which uses the DHT P2P network to find other
torrent clients with that file and download the .torrent file from
them. The original web server only gave you the original URL, and isn't
involved in you fetching that content.

So, magnet URLs have the advantage that they don't require the server to
actually serve up the .torrent files, and they give an easy way for
users to share links to torrents instead of having to share the entire
.torrent file. The original web server can be years dead, yet the magnet
URL can still keep working as long as there are users out there with
that file.

---

Short version:

Instead of downloading the .torrent file from a webserver, you download
it directly from a seed/leecher. The biggest advantage is that you might
be able to download the content of the torrent, even if the tracker is
down or closed for registration.

Long version:

Traditionally, .torrent files are downloaded from torrent sites. A
torrent client then calculates a torrent hash (a kind of fingerprint)
based on the files it relates to, and seeks the addresses of peers from
a tracker (or the DHT network) before connecting to those peers and
downloading the desired content.

Sites can save on bandwidth by calculating torrent hashes themselves and
allowing them to be downloaded instead of .torrent files. Given the
torrent hash – passed as a parameter within a Magnet link – clients
immediately seek the addresses of peers and connect to them to download
first the torrent file, and then the desired content.

It is worth noting that BitTorrent can not ditch the .torrent format
entirely and rely solely on Magnet links. The .torrent files hold
crucial information that is needed to start the downloading process, and
this information has to be available in the swarm.
```

# BitTorrent Clients

## libtorrent library

- https://www.libtorrent.org/
    + libtorrent is a feature complete C++ bittorrent implementation
      focusing on efficiency and scalability
- https://github.com/arvidn/libtorrent

## qBittorrent

- It uses libtorrent library
- https://www.qbittorrent.org/
- https://github.com/qbittorrent/qBittorrent/wiki/

### Options and Settings

+ https://github.com/qbittorrent/qBittorrent/wiki/Explanation-of-Options-in-qBittorrent
+ Bind to VPN network interface to prevent IP leaks
    * https://raw.githubusercontent.com/wiki/qbittorrent/qBittorrent/How-to-bind-your-vpn-to-prevent-ip-leaks.md
    * Go to `Options -> Advanced -> Network interface` and select
      VPN interface.
    * This is not necessary if we run qBittorrent as docker
      container and the container is only using VPN network
      interface.

#### Connections

- https://forum.qbittorrent.org/viewtopic.php?t=6017

```
Max connections per torrent is the max number of peers that can be connected at once on a single torrent even when there's more peers trying to connect.

Max number of upload slots per torrent is how may of the connected peers qBitTorrent tries to upload to at once (the rest are effectively queued OR ignored completely).
Basically, how thinly you are spreading your upload speed around.

If you have 100 KB/sec upload speed max and allow 100 connections per torrent AND have upload slots per torrent also set to 100 (or don't have a limit on upload slots globally or per torrent), then qBitTorrent will try to upload to every connected peer on a torrent. Average upload speed per peer will be maybe 1 KB/sec at best ...and if you're downloading that torrent many of those peers will SNUB (ignore) your peer and not upload back.

Peers upload almost entirely to the OTHER peers that give them the most back, up to the limit of the number of upload slots they allow. They try to automatically reward the "givers" and ignore the "takers". Most BitTorrent clients limit upload slots per torrent to only 4. For really fast internet connections, you want to be one of their 4 upload slots! But that means you have to upload slightly more to them than almost all other peers. This can be as little as 10 KB/sec to them on public torrents with lots of ADSL-using peers. If you have only 100 KB/sec upload speed max, then 10 KB/sec is 1/10th of that ...so upload slots should be 10 at most spread between all your torrents. So probably BOTH the global upload slot limit as well as the per torrent upload slots should be no greater than 10.
```
