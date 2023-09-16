# Overview

- https://en.wikipedia.org/wiki/BitTorrent
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

# Torrent files

- https://en.wikipedia.org/wiki/Torrent_file
- A torrent file contains a list of files and integrity metadata about
  all the pieces, and optionally contains a large list of trackers.

# Private Trackers

- An accurate description would separate private trackers into 2 parts:
  the tracker itself and the website that accompanies it.
    + A torrent tracker is a server that tracks peers in a torrent swarm
      and assigns/connects peers to each other based on its own internal
      criteria.
    + The tracker then reports to the website which, on top of providing
      a download link to the torrent file, will display all relevant
      info for that torrent, including peer/seed counts and optionally a
      peer list if the website operator chooses to include it.
- Unlike public trackers, these are not a free-for-all buffet. You need
  to contribute back (by uploading) a certain amount proportional to the
  amount you have "taken" from the tracker. This arrangement can vary a
  lot from tracker to tracker. Private trackers track this balance of
  contribution by a "ratio", which is simply a ratio of uploaded data,
  divided by your downloaded data. If you downloaded a total of 2GB and
  uploaded a total of 4GB, that would make your ratio a 2.0. Trackers
  will sometimes have different methods of maintaining an acceptable
  ratio, either by offering bonuses the longer you keep your torrents
  seeding, to providing "half-leech" or "freeleech" content. Freelech
  content is the most commonly used method, which means the torrent that
  is marked as freeleech is free to download, meaning it does not count
  against your Download stats, giving you an opportunity to gain upload
  from it without sacrificing any "download buffer". Some torrent
  trackers are "ratioless", meaning they don't require you to maintain
  any sort of ratio in order to keep using the site, they just require a
  minimum seed-time on all downloaded torrents (which is usually also a
  requirement on ratio pure trackers, but typically the seed-time isn't
  as lengthy as on ratioless trackers).
