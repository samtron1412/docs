[TOC]

# Overview

- IRC Protocol Standard:
    + RFC 1459: original
    + Revised protocol: RFC 2810, RFC 2811, RFC 2812, RFC 2813 (however
      these changes have not been widely adopted among implementations)
    + The protocol remains dynamic.
- Orignallly, IRC was a plain text protocol over TCP, but now it
  supports TLS.

# Concepts

## Network Structure

+ Servers connect to each other to form a network.
+ Clients connect to servers to communicate.
+ The server network structure  is a tree. Messages are routed along
  only necessary branches of the tree but network state is sent to
  every server.
+ However, this architecture has a number of problems.
    * A misbehaving or malicious server can cause major damage to
      the network[40] and any changes in structure, whether
      intentional or a result of conditions on the underlying
      network, require a net-split and net-join.
    * This results in a lot of network traffic and spurious
      quit/join messages to users[41] and temporary loss of
      communication to users on the splitting servers.
    * Adding a server to a large network means a large background
      bandwidth load on the network and a large memory load on the
      server.
+ Once established, however, each message to multiple recipients is
  delivered in a fashion similar to multicast, meaning each message
  travels a network link exactly once.[42] This is a strength in
  comparison to non-multicasting protocols.

## Commands and replies

- Clients send single-line messages to the server, receive replies to
  those messages and receive copies of some messages sent by  other
  clients.
- In most clients, users can enter commands by prefixing them with a
  `/`.
    + Depending on the command, these may either be handled entirely by
      the client, or passed directly to the server.

### List of IRC Commands

- https://en.wikipedia.org/wiki/List_of_IRC_commands

### Queries / Private Messages / Direct Messages (DM)

## Channels

- The basic means of communicating to a group of users in an established
  IRC session is through a channel.
- List of channels can be displayed with command `/list`:
    + List all available channels that do not have the modes `+s` or
      `+p` set, on that particular network.
- Join a channel with `/join #channel` command.
- Channels that are available across an entire IRC network are prefixed
  with `#`, while those local to a server  use `&`.
    + Other less common channel types:
        * `+`: modeless channels without operators
        * `!`: a form of timestamped channel on normally non-timestamped
          networks.

## Modes

- Users and channels may have `modes` that are represented by individual
  case-sensitive letters and are set using the `/mode` command.
- User modes
    + `i`: invisible (cannot be seen without a common channel or
      knowing the exact name)
    + `s`: receives server notices
    + `w`: receives wallops
    + `o`: user is an IRC operator (ircop)
- Channel modes:
    + `o`: symbol `@`, parameter(s): name of affected user: channel
      operator, can change channel modes and kick users out of the
      channel, etc.
    + `s`: secret channel: not shown in channel list or user whois
      except to users already on the channel.
    + `p`: private channel: listed in channel list as "prv"
    + `n`: users cannot send messages to the channel externally
    + `m`: channel is moderated (only those who hold channel operator or
      voice status on the channel can send messages to it)
    + `i`: only users with invites may enter the channel
    + `t`: only channel operators can change the channel topic
    + `l`: parameter: limit number: limits number of users able to be on
      channel  (when full, no new users can join)
    + `b`: parameter: ban mask (nick!user@host with wildcards allowed):
      bans hostmasks from channel
    + `v`: symbol: `+`, parameters: name of affected user: gives a user
      voice status on channel
    + `k`: parameter: new channel key: sets a channel key such that only
      users knowing the key can enter

## Channel operators

- Can manage channel: kick/ban users, etc.

## IRC Operators

- Have admin rights on their local server or the entire network:
    + Disconnect / connect servers.
    + Disconnect clients / ban IP addresses or complete subnets.

##  Hostmasks

- A hostmask is a unique identifier of an IRC client connected to an IRC
  server.
    + `nick!user@host` pattern
    + `nick`: nick chosen by  the user and may be changed while
      connected
    + `user` is the user name reported by ident on the client.
    + `host`: the hostname the client is connecting from. if the IP
      address of the client cannot be resolved to a valid hostname by
      the server, it is used instead of the hostname.
- Some IRC daemons hash these hostmasks to protect identities. (only
  IRCops users can access)

## URI scheme

```
irc://<host>[:<port>]/[<channel>[?<channel_keyword>]]
ircs://<host>[:<port>]/[<channel>[?<channel_keyword>]]
irc6://<host>[:<port>]/[<channel>[?<channel_keyword>]]
```

## Clients

### Client Software

- WeeChat, hexChat, irssi, etc.

### Bots

- A set of scripts or an independent program that connects to IRC as a
  client to perform automated functions.

### Bouncer

- A program that runs as a daemon on a server and functions as a
  persistent proxy.
- The purpose is to maintain a connection to an IRC server, acting as a
  relay between the server and client, or simply to act as a proxy.
- Should the client lose network connectivity, the BNC may stay
  connected and archive all traffic for later delivery, allowing the
  user to resume their IRC session without disrupting their connection
  to the server.
- We can simulate this behavior by installing IRC client on always-on
  server and connect to it through SSH from other machines.

# Authentication

## SASL (Simple Authentication and Security Layer)

- An extension (part of IRCv3) that allows clients to securely
  authenticate with services like NickServ during the connection
  process.
- It eliminates the need for `/msg NickServ IDENTIFY` after joining,
  ensuring authentication occurs before your nick is fully active.

## NickServ

- Set desired nickname: `/nick YourNick`
- Register
    + `/msg NickServ register YourPassword youremail@example.com`
- Identify / Log in (better to use SASL if it's available)
    + `/msg NickServ identify YourNick YourPassword`
- Group nicks:
    + `/nick YourNick2`
    + `/msg NickServ identify YourNick YourPassword`
    + `/msg NickServ group`

# History

## Freenode to Libera

- https://lwn.net/Articles/857140/
- https://nedbatchelder.com/blog/202106/goodbye_freenode
- https://news.ycombinator.com/item?id=27491967
- https://www.reddit.com/r/linux/comments/wv8wjq/what_exactly_provoked_the_mass_migration_from/


# Related Protocols

## Ident protocol

- https://en.wikipedia.org/wiki/Ident_protocol
- The Ident protocol (Identification Protocol, often just ident) is an
  application-layer protocol specified in RFC 1413.
    + Given a pair of TCP port numbers corresponding to an existing
      connection, an Ident server returns a short string that identifies
      the owner of that connection on the server’s host.
    + The protocol listens on TCP port 113.

## Client To Client Protocol (CTCP) and Direct Client To Client (DCC)

- https://en.wikipedia.org/wiki/Client-to-client_protocol
- https://en.wikipedia.org/wiki/Direct_Client-to-Client
- CTCP extends the original IRC protocol by allowing users to query
  other clients or channels, this causes all the clients in the channel
  to reply the CTCP, for specific information.
- DCC allows to transfers files.

## Extended DCC (XDCC)

- Allow to transfer large files or group of files.

# References
1. [Wikipedia - Internet Relay Chat][1]
2. [Demo IRC network][2]

[1]: https://en.wikipedia.org/wiki/Internet_Relay_Chat "Wikipedia - Internet Relay Chat"
[2]: http://pdgn.co/ "Demo IRC network"
