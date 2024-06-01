# Introduction

[Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)  (SSH) is a
**network protocol**  for **secure data communication**, **remote shell
services** or **command execution** and other secure network services
between two networked computers that it connects via a secure channel
over an insecure network: a server and a client. Best known application
is **access to shell account** of Unix-like operating systems. It was
designed as a replacement for
[Telnet](https://en.wikipedia.org/wiki/Telnet) and other insecure remote
shell protocols such as the Berkeley
[rsh](https://en.wikipedia.org/wiki/Remote_Shell) and
[rexec](https://en.wikipedia.org/wiki/Remote_Process_Execution)
protocols. The encryption used by SSH is intended to provide
**confidentiality** and **integrity** of data over an unsecured network,
such as the Internet.

There are several ways to use SSH; one is to use *automatically
generated public-private key pairs* to simply encrypt a network
connection, and then use *password authentication* to log on.

SSH is typically used to log into a remote machine and execute commands,
but it also supports
[tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol),
forwarding TCP ports and X11 connections; it can transfer files using
the associated [SSH file
transfer](https://en.wikipedia.org/wiki/SSH_file_transfer_protocol)
(SFTP) or [secure copy](https://en.wikipedia.org/wiki/Secure_copy) (SCP)
protocols. SSH uses the client-server model

SSH is organized as three protocols that typically run on top of TCP.
- TCP (Transport Layer Protocol): provides server authentication, data
  confidentiality, and data integrity with forward secrecy.
    + Establish TCP connection and Key exchange (math)
- User Authentication Protocol: authenticates the user to the server.
- Connection Protocol: multiplexes multiple logical communications
  channels over a single, underlying SSH connection.

# User guide

## OpenSSH Client

### `ssh` command to start the client

- `man ssh`
- https://www.ssh.com/academy/ssh/command

### OpenSSH Client Configuration

- `man ssh_config`
- https://sthbrx.github.io/blog/2023/08/04/quirks-of-parsing-ssh-configs/
    + Very good article to understand SSH config parsing rules.
- SSH Configuration parsing rules
    1. For starters, the config is parsed line by line. Leading
       whitespace (i.e., indentation) is ignored. So, while indentation
       makes it look like you are configuring properties for a
       particular host, this isn't quite correct. Instead, the Host and
       Match lines are special statements that enable or disable all
       subsequent lines until the next Host or Match.
        - There is no backtracking; previous conditions and lines are
          not re-evaluated after learning more about the config later
          on.
    2. When a config line is seen, and is active thanks to the most
       recent Host or Match succeeding, its value is selected if it is
       the first of that config to be selected. So the earliest place a
       value is set takes priority.
        -  Since the first obtained value for each parameter is used,
           more host-specific declarations should be given near the
           beginning of the file, and general defaults at the end.
    3. When `HostName` is set, it replaces the `host` value in `Match`
       matches. It is also used as the `Host` value during a final pass
       (if requested).
        - Host name that is used in `Host` is normally the hostname
          parameter in command line, but it can be the `HostName` value
          in the second parsing.
    4. The last behavior of interest is the `Match final` rule. There
       are several conditions a Match statement can have, and the final
       rule says make this active on the final pass over the config.
        - This will make the configuration to re-parse the second time.
- Best practices
    + Having `Match final` at the beginning to always keep the same
      parsing behavior. Parsing twice.
    + Putting more host-specific on top, and general defaults at the
      bottom.
    + Use `Host` for host-specific, and `Match host` for more general
      defaults.

## OpenSSH Server

### `sshd` server process

- `man sshd`
- https://www.ssh.com/academy/ssh/sshd

### OpenSSH Server Configuration

- `man sshd_config`
- [config on RHEL](http://computernetworkingnotes.com/network-administration/how-to-configure-ssh-server-in-rhel-6.html)


## SSH Keys

- https://www.ssh.com/academy/ssh-keys
- https://security.stackexchange.com/questions/50878/ecdsa-vs-ecdh-vs-ed25519-vs-curve25519

## Opening a Terminal on a remote machine through SSH

The syntax: `ssh username@hostname`

where username is the name of your account on the remote system and
hostname is the hostname of remote system.

`ssh -i <file private key> username@hostname` : authentication by private key.

## Transferring files with SSH

There are two main command line SSH commands to transfer files: **scp**
and **sftp**.

**scp** is a non-interactive command that takes a set of files to copy
on the command line, copies them, and exits. **sftp** is an interactive
command that opens a persistent connection that multiple copying
commands can be performed through.

### scp

```
scp local_file(s) user@hostname:destination_directory

[abc123@funkmachine ~]$ scp foo.c foo.h abc123@lionxj.rcc.psu.edu:.

[abc123@funkmachine ~]$ scp -r srcdir abc123@hammer.rcc.psu.edu:.

scp jwh128@lionxi.rcc.psu.edu:results.txt .
```

### sftp

There are a number of basic commands that are used inside of stfp:
- **put** filename: uploads the file filename
- **get** filename: downloads the file filename
- **ls**: lists the contents of the current remote directory
- **lls**: lists the contents of the current local directory
- **pwd**: returns the current remote directory
- **lpwd**: returns the current local directory
- **cd** directory: changes the current remote directory to directory
- **lcd** directory: changes the current local directory to directory

        sftp username@hostname

## SSH with git

Check directory .ssh at your account directory. If don't have a default
identity of SSH then create new one:

        ssh-keygen

        ssh-keygen -t rsa/dsa -C "email@email.com"

Start agent and add key to agent

        ssh-agent /bin/bash

        ssh-add ~/.ssh/id_rsa

List key agent managing

        ssh-add -l



## Other Commands

### ssh-keygen

### ssh-agent

### ssh-add


# SSH tunneling (SSH port forwarding)

- https://serverfault.com/a/1053450/220364
- https://goteleport.com/blog/ssh-tunneling-explained/

## What, Why, and How

- https://www.ssh.com/academy/ssh/tunneling
- What
    + SSH tunneling is a method to transport additional data streams
    + SSH port forwarding is a mechanism in SSH for forwarding
      (tunneling) application ports from the client machine to the
      server machine, or vice versa.
- Why
    + Adding encryption to legacy applications.
    + Going through firewalls.
    + Opening backdoor into the internal network from home machines.

## How: SSH tunneling example

### Local Forwarding

- Forward a port from the client machine to the server machine.
    + The SSH client
- `ssh -L localhost:8080:intra.example.com:8080 remotehost`
- `ssh -L localhost:8080:localhost:8080 clouddesk`
    + Forward connections to `localhost:8080` on your local computer to
      `localhost:8080` on the remote computer.

### Remote Forwarding

- `ssh -R 8080:localhost:80 public.example.com`

### Dynamic Port Forwarding

- server side configuration
    + `AllowTcpForwarding`: required
    + Other related configurations: `AllowStreamLocalForwarding`,
      `GatewayPorts`
- `ssh -D port-number user@<ssh-server>`
    + `port-number`: localhost port-number that will be used for the
      local SOCKS proxy server.
    + `user`: a user on the SSH server
    + `<ssh-server>`: IP address or SSH server name configured in
      `ssh_config`

### SSH TUN/TAP tunneling

- https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Proxies_and_Jump_Hosts#Passing_Through_a_Gateway_with_an_Ad_Hoc_VPN
- https://www.marcfargas.com/2008/07/ip-tunnel-over-ssh-with-tun/

### SSH tunnel over TOR

-

# SSH protocol

- https://www.ssh.com/academy/ssh/protocol
- SSH algorithms
    + https://security.stackexchange.com/questions/50878/ecdsa-vs-ecdh-vs-ed25519-vs-curve25519
    + Key exchange algorithms: DH (Diffie-Hellman) or ECDH
      (Elliptic Curve Diffie-Hellman)
    + Signature algorithms: DSA, RSA, ECDSA, Ed25519

# Tips and Tricks

## Forward local ssh-agent to the remote machine

- With this forward agent, the remote machine does not need to have its
  own ssh-agent running

```
Host clouddesk
   HostName host.us-east-1.amazon.com
   User username
   ForwardAgent yes
```
