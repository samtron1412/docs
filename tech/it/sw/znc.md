# Overview

- https://wiki.znc.in/ZNC
- ZNC is an IRC bouncer that allows always connect to IRC networks and
  channels and keeping chat logs.
- Clients can then connect to this bouncer to get chat messages later.
    + The Lounge web client, WeeChat, etc.

# Modules

- https://wiki.znc.in/Ctcp_Notifier
- To set arguments for the module in webadmin:
    + Using the argument box and add the arguments space-separated: arg1
      arg2 arg3 ...
- To change arguments for already loaded module, you need to unload
  (uncheck), save, and then reload it with the new arguments filled in.

# Connecting to ZNC

- Password to connect: `zncuser/zncnetwork:password`

# IRC Ident in ZNC

The ident (also called "username" in IRC protocol) is the part that appears before the @ in your IRC hostmask:

nick!ident@host

For example, if your hostmask is glider!~glider@192.168.1.1, then glider is the ident.

Where it's set in ZNC

- Per-user level: The Ident setting in your ZNC user config
- Per-network level: Can be overridden with Ident under a specific network block

In znc.conf it looks like:

<User glider>
  Ident = glider
  <Network libera>
      Ident = myident   # overrides user-level for this network only
  </Network>
</User>

What it does

- Sent to the IRC server during connection as part of the USER command
- If the server runs an identd check (port 113), your ident may be replaced by the system-level response — ZNC has an identfile module to handle this
- If identd fails, most servers prepend a ~ to indicate an unverified ident (hence ~glider)

Practical notes

- Most people just set it to their nick and leave it alone
- It's cosmetic on most modern networks — servers rarely enforce it
- Some networks use it for bans (*!badident@*), so keep it consistent

# BindHost

  The local IP address ZNC uses when connecting outbound to IRC servers.

  This matters when your machine has multiple IP addresses/interfaces. By default ZNC uses whatever the OS picks. Setting BindHost forces it to use a specific one.

  nick!ident@bindhost.resolved.rdns

  Why you'd set it:
  - Server has multiple IPs and you want a specific reverse DNS (vhost) to appear as your hostname
  - Network routing requirements — force traffic through a specific interface
  - Running multiple ZNC users and want each to appear from a different IP

  Levels it can be set at:
  - Global — default for all users
  - Per-user — overrides global
  - Per-network — overrides user

  <User glider>
      BindHost = 203.0.113.10
      <Network libera>
          BindHost = 203.0.113.11   # different IP for this network
      </Network>
  </User>

## DCCBindHost

  The IP address advertised in DCC connections (direct file transfers and DCC chat).

  DCC works by telling the other person "connect to me at this IP on this port." If your ZNC is behind NAT or has multiple IPs, the auto-detected address might be wrong.

  <User glider>
      DCCBindHost = 203.0.113.10
  </User>

  Key differences

  ┌─────────────┬───────────────────────────────┬────────────────────────────────┐
  │             │           BindHost            │          DCCBindHost           │
  ├─────────────┼───────────────────────────────┼────────────────────────────────┤
  │ Purpose     │ Outbound connection source IP │ IP advertised for DCC          │
  ├─────────────┼───────────────────────────────┼────────────────────────────────┤
  │ Affects     │ Your visible hostname on IRC  │ Direct file transfers/DCC chat │
  ├─────────────┼───────────────────────────────┼────────────────────────────────┤
  │ When needed │ Multiple IPs / vhost control  │ NAT / multiple IPs + DCC usage │
  └─────────────┴───────────────────────────────┴────────────────────────────────┘

  For most people

  - Single IP, no DCC: Leave both blank — ZNC handles it automatically
  - Multiple IPs / want specific vhost: Set BindHost to the desired IP
  - Use DCC behind NAT: Set DCCBindHost to your public IP

  DCC is rarely used on modern IRC, so DCCBindHost is mostly irrelevant unless you specifically transfer files over IRC.

# CTCP Modules

- https://wiki.znc.in/Ctcpflood
- https://wiki.znc.in/Ctcp_Notifier
