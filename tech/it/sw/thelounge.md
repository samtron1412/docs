# Overview

- IRC Web Client
- https://thelounge.chat/
- IRC Web client
- Modes:
    + Private mode: The Lounge acts like a bouncer and a client
      combined.
        * Users can then access and resume their session without being
          disconnected from their channels.
    + Public mode: it acts as an open chat available to anyone without
      registration.

# Configurations

- https://thelounge.chat/docs/configuration

## Server Settings

- public
- host
- port
- bind
- reverserProxy
- maxHistory
- https

## Client Settings

- theme
- prefetch
- disableMediaPreview
- prefetchStorage
- prefetchMaxImageSize
- prefetchMaxSearchSize
- prefetchTimeout
- fileUpload
- transports
- leaveMessage

## Default Network

- defaults

## User Management

- `messageStorage`
    + Log messages to access later.
    + Default: `["sqlite", "text"]`
    + "sqlite": messages stored in SQLite database files, one per user
    + "text": messages per network and channel will be stored as text
      files. Messages will not be reloaded on restart.
- `storagePolicy`

# Users

- https://thelounge.chat/docs/users
- Listing all users: `thelounge list`
- Adding a user: `thelounge add <name>`
    + Logs are stored at: `${THELOUNGE_HOME}/users/`
- Removing a user: `thelounge remove <name>`
    + This does not delete the logs for this user.
- Resetting a user's password: `thelounge reset <name>`
- Editing a user configuration file: `thelounge edit <name>`
    + Config file at: `${THELOUNGE_HOME}/users/<name>.json`
    + Apart from password field, all changes to the configurations file
      will require a server restart to take effect.

# Guides

## CTCP

- https://thelounge.chat/docs/guides/ctcp
- The Lounge does not support all CTCP commands such as DCC.

## ZNC  bouncer

- https://thelounge.chat/docs/guides/znc
- Load `clientbuffer` and `savebuff` modules.
- In order to connect, you will need to specify the server you want to
  use in the username field.
    + Within the server settings of The Lounge directly:
        * Username: zncUser/network
        * Password: zncPassword
    + Or if you are using the Clientbuffer module:
        * Username: zncUser@clientid/network
        * Password: zncPassword
