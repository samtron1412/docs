[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/Mutt_(email_client))

Text-base Mail Client. Mutt focuses primarily on being a **Mail User Agent (MUA)**, and was originally written to *view mail*. Later implementations (added for retrieval, sending, and filtering mail) are simplistic compared to other mail applications and, as such, users may wish to use external applications to extend Mutt's capabilities.

## Resources
- [Manual](http://www.mutt.org/doc/manual/)
- `man mutt` and `man muttrc`

# Configuring
## Native IMAP
```
# Gmail requires full email address (this is not a standard)
set imap_user=samtron1412@gmail.com

# If unset, the password will be prompted for
set imap_pass=$my_pw_personal

# set folder=imap[s]://imap.server.domain[:port]/[folder/]
set folder = imaps://samtron1412@imap.gmail.com:993/

# The spoolfile is the folder where your (unfiltered) e-mail arrives.
set spoolfile = +INBOX

# check for all subscribed IMAP folders
# set imap_check_subscribed

# Any imap folders that should be checked regularly for new mail should be listed here:
# mailboxes =INBOX =family
# mailboxes imaps://imap.gmail.com/INBOX imaps://imap.gmail.com/family
# the 'y' key which will allow you to change to any of the folders listed under mailboxes.
```

## SMTP
Whether you use POP or IMAP to receive mail you will probably still send mail using SMTP.

### Folder: the one where all your sent e-mails will be saved
- `set record = +Sent`
- Gmail saves automatically sent e-mail to `+[Gmail]/Sent`, so we do not want duplicates. `unset reccord`

### Native SMTP support

```
set my_pass='mysecretpass'
set my_user=myname

set realname = 'Your Real Name'
set from = your-email-address
set use_from = yes

set smtp_url=smtps://$my_user:$my_pass@smtp.domain.tld
set ssl_force_tls = yes

set ssl_starttls = yes
```

You may need to tweak the security parameters. If you get an error like `SSL routines:SSL23_GET_SERVER_HELLO:unknown protocol`, then your server probably uses the SMTP instead of SMTPS.
`set smtp_url=smtp://$imap_user:$imap_pass@smtp.domain.tld`

`man 5 muttrc` for more information.

## Multiple accounts
All the IMAP/SMTP config for each account should go to its respective folder.

>**Warning:** When one account is setting a variable that is not specified for other accounts, you **must unset** it for them, otherwise configuration will overlap and you will most certainly experience unexpected behavior.

Mutt can handle this by its hooks. Basically a hook is a command that gets executed before a specific action. There are several hooks available. For multiple accounts, you must use account-hooks and folder-hooks.
- Folder-hooks will run a command before switching folders. This is mostly useful to set the appropriate SMTP parameters when you are in a specific folder. For instance when you are in your work mailbox and you send a e-mail, it will automatically use your work account as sender.
- Account-hooks will run a command everytime Mutt ccalls a function related to an account, like IMAP syncing. It does not require you to switch to any folder.

Hooks take two parameters:

	account-hook [!]regex command
	folder-hook [!]regex command

The regex is the folder to be matched (or not if preceded by the `!`). The command tells what to do.

Example: `muttrc`

	## General options
	set header_cache = "~/.cache/mutt"
	set imap_check_subscribed
	set imap_keepalive = 300
	unset imap_passive
	set mail_check = 60
	set mbox_type=Maildir

	## ACCOUNT1
	source "~/.mutt/work"
	# Here we use the $folder variable that has just been set in the sourced file.
	# We must set it right now otherwise the 'folder' variable will change in the next sourced file.
	folder-hook $folder 'source ~/.mutt/work'

	## ACCOUNT2
	source "~/.mutt/personal"
	folder-hook *user@gmail.com/ 'source ~/.mutt/personal'
	folder-hook *user@gmail.com/Family 'set realname="Se"'

`.mutt/work`

	## Receive options.
	set imap_user=user@gmail.com
	set imap_pass=****
	set folder = imaps://user@imap.gmail.com/
	set spoolfile = +INBOX
	set postponed = +Drafts
	set record = +Sent

	## Send options.
	set smtp_url=smtps://user:****@smtp.gmail.com
	set realname='User X'
	set from=user@gmail.com
	set hostname="gmail.com"
	set signature="John Doe"
	# Connection options
	set ssl_force_tls = yes
	unset ssl_starttls

	## Hook -- IMPORTANT!
	account-hook $folder "set imap_user=user@gmail.com imap_pass=****"

To switch from one account to another, just change the folder (`c` key). To change folder for different mailboxes you have to type the complete address -- let us bind some key to it.

	## Changing accounts
	macro index,pager <f2> '<sync-mailbox><enter-command>source ~/.mutt/personal<enter><change-folder>!<enter>'
	macro index,pager <f3> '<sync-mailbox><enter-command>source ~/.mutt/work<enter><change-folder>!<enter>'

With the above shortcuts you will find that changing folders (with `c`) is not contextual, i.e. it will not list the folders of the current mailbox, but of the one had used the last time before you changed folders. To make the behavior more contextual, the trick is to press `=` or `+` for current mailbox. You can automate this with the following macro:

	macro index 'c' '<change-folder>?<change-dir><home>^K=<enter>'

## Password management

# Advanced features
## Key bindings

## E-mail character encoding

## Printing

## Custom mail headers

## Signature block

## Viewing URLs

## Viewing HTML

## Mutt and Vim

## Colors

## Index Format

## Contact management

## Request IMAP mail retrieval manually

## Avoiding slow index on large (IMAP) folders due to coloring

## Speed up folders switch

## Composing HTML e-mails

## Archive treated e-mails

## Migrating e-mails from one computer to another

## Filtering the message view

## Display the index above the pager view

## Default folder for saving attachments

## PGP signed/encrypted e-mails

## Pager behavior

## Fast reply

## Ignore own e-mail addresses from group-reply

## Conversation grouping

## IMAP message cache
