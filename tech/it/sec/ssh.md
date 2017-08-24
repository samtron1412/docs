# Introduction
[Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)  (SSH) is a  **network protocol**  for **secure data communication**, **remote shell services** or **command execution** and other secure network services between two networked computers that it connects via a secure channel over an insecure network: a server and a client. Best known application is **access to shell account** of Unix-like operating systems. It was designed as a replacement for [Telnet](https://en.wikipedia.org/wiki/Telnet) and other insecure remote shell protocols such as the Berkeley [rsh](https://en.wikipedia.org/wiki/Remote_Shell) and [rexec](https://en.wikipedia.org/wiki/Remote_Process_Execution) protocols. The encryption  used by SSH is intended to provide **confidentiality** and **integrity** of data over an unsecured network, such as the Internet.

There are several ways to use SSH; one is to use *automatically generated public-private key pairs* to simply encrypt a network connection, and then use *password authentication* to log on.

SSH is typically used to log into a remote machine and execute commands, but it also supports [tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol), forwarding TCP ports and X11 connections; it can transfer files using the associated [SSH file transfer](https://en.wikipedia.org/wiki/SSH_file_transfer_protocol) (SFTP) or [secure copy](https://en.wikipedia.org/wiki/Secure_copy) (SCP) protocols. SSH uses the client-server model

<figure>
  <figcaption style="text-align:center;">SSH packet</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="Ssh_binary_packet.png" alt="ssh binary packet" title="ssh binary packet">
</figure>

SSH is organized as three protocols that typically run on top of TCP.
- Transport Layer Protocol: provides server authentication, data confidentiality, and data integrity with forward secrecy.
	+ Establish TCP connection
	+ Key exchange (math)
- User Authentication Protocol: authenticates the user to the server.
- Connection Protocol: multiplexes multiple logical communications channels over a single, underlying SSH connection.

# User guide
## Configuration
System wide: `/etc/ssh/sshd_config`
Each user: `~/.ssh/config`

- [config on RHEL](http://computernetworkingnotes.com/network-administration/how-to-configure-ssh-server-in-rhel-6.html)

## Opening a Terminal on a remote machine through SSH
The syntax:

	ssh username@hostname

where username is the name of your account on the remote system and hostname is the hostname of remote system.

`ssh -i <file private key> username@hostname` : authentication by private key.

## Transferring files with SSH
There are two main command line SSH commands to transfer files: **scp** and **sftp**.

**scp** is a non-interactive command that takes a set of files to copy on the command line, copies them, and exits. **sftp** is an interactive command that opens a persistent connection that multiple copying commands can be performed through.

### scp
	scp local_file(s) user@hostname:destination_directory

	[abc123@funkmachine ~]$ scp foo.c foo.h abc123@lionxj.rcc.psu.edu:.

	[abc123@funkmachine ~]$ scp -r srcdir abc123@hammer.rcc.psu.edu:.

	scp jwh128@lionxi.rcc.psu.edu:results.txt .

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
Check directory .ssh at your account directory. If don't have a default identity of SSH then create new one:

	ssh-keygen

	ssh-keygen -t rsa/dsa -C "email@email.com"

Start agent and add key to agent

	ssh-agent /bin/bash

	ssh-add ~/.ssh/id_rsa

List key agent managing

	ssh-add -l

	