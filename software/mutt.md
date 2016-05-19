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

## Maildir

## SMTP

## Multiple accounts

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
