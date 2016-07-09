[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/Mutt_(email_client))

Text-base Mail Client. Mutt focuses primarily on being a **Mail User Agent (MUA)**, and was originally written to *view mail*. Later implementations (added for retrieval, sending, and filtering mail) are simplistic compared to other mail applications and, as such, users may wish to use external applications to extend Mutt's capabilities.

## Resources
- [Manual](http://www.mutt.org/doc/manual/)
- `man mutt` and `man muttrc`


## Core concepts
Mutt is configured through variables which are written to configuration files (`~/.mutt/muttrc`).

`functions` which can be executed manually (using the command lines) or in macros.

`macros` allow the user to bind a sequence of commands to a single key or a short key sequence instead of repeating a sequence of actions over and over.

`tagged` messages: a set of messages, to help selecting messages, Mutt provides a rich set of message patterns (such as recipients, sender, body contents, date sent/received, etc.) which can be combined into complex expressions using the boolean `and` and `or` operations as well as negating. These patterns can also be used to search for messages or to limit the index to show only matching messages.

`hook` allows the user to execute arbitrary configuration commands and functions in certain situations such as entering a folder, starting a new message or replying to and existing one. These hooks can be used to highly customize Mutt's behavior including managing multiple identities, customizing the display for a folder or even implementing auto-archiving based on a per-folder basis and much more.

`command line options`

## User interface
You can always type `?` in any menu to display the current bindings.

Invoke Mutt simply by typing `mutt` at the command line.

A line-based menu is the so-called `index` menu (listing all messages of the currently opened folder) or the `alias` menu (allowing you to select recipients from a list). Examples for page-based menus are the `pager` (showing one message at a time) or the `help` menu listing all available key bindings.

The **user interface** consists of:
- **a context sensitive help line** at the top
- the **menu's contents**
- **a context sensitive status line**
- the **command line**. The command line is used to display informational and error messages as well as for prompts and for entering interactive commands.

### The `index` viewer
When you launch mutt, the first thing you see is a screen with a list of email messages. This initial screen is called the `index`.

These messages are in a default mail folder, often called the `mailspool` that you can think of as you `inbox`. Use the `k` and `j` keys to move the highlighted cursor up and down the list of messages.

The information you see in the index is a list of emails:
- each with its number on the left
- its flags (new email, important email, email that has been forwarded or replied to, tagged email, ...)
- the date when email was sent
- its sender
- the email size
- the subject
- Additionally, the index also shows thread hierarchies. This is especially useful for personal email between a group of people or when you've subscribed to mailing lists.

### The `pager`
If you are in the `index` and you want to view the contents of an email, hit the `enter` key, this will take you from the `index` to the `pager`. Mutt's built-in `pager` is just a scrolling text viewer like the unix programs `more` and `less`, use the `backspace` and `enter` keys to scroll up and down the email. Quit the `pager` and return to the `index` by pressing the `q` key.

On the top of the pager you have an overview over the most important email headers: the sender, the recipients, the subject, etc. How much information you actually see depends on your configuration.

Below the headers, you see the email body which usually contains the message. If the email contains any attachments, you will see more information about them below the email body, or, it the attachments are text files, you can view them directly in the pager.

### The `attachment` viewer
E-mail has a structure that can include attached parts such as files as well as plain text messages. From the `index`, press the `v` key to view the `attach` menu where you can see the `mime-structure` of the email displayed as a threaded list.

If there is more than one part to a message, you can use the `k` and `j` keys to move up and down the list and the `enter` key to view any item. If the attachment can be viewed by mutt's internal `pager` as plain text then it will. If not, mutt will try and launch a suitable external viewer, and wait for it to finish.

Quit the `attachment` viewer by pressing the `q` key.

### The file `browser`
To change from your mailspool to a different mailfolder, press the `c` key. You can now either type in the location of the folder you want to open, or press the `?` key to open the file `browser`. Use the `k` and `j` keys to select the folder you want to switch-to and open it by hitting the `enter`.

### The `editor`
In the `index` or `pager` views, hit the `r` key to reply to a message or the `m` key to create a new one. Mutt will prompt for the `To:` address and the `Subject:` line, then launch your favorite text editor (defined by your $EDITOR environmental variable). Type away, when you save and exit, you are done.

### The `compose` menu
After the editor, mutt drops you into the `compose` menu, here you can fine-tune your message headers, change the encoding, add file attachments or simply hit the `y` key to say yes and send your email on its way.

# Getting Started
## Moving around in menus
**Most common navigation keys in entry-based menus (line-based)**

| Key           | Function         | Description                                |
| j or <Down>   | <next-entry>     | move to the next entry                     |
| k or <Up>     | <previous-entry> | move to the previous entry                 |
| z or <PageDn> | <page-down>      | go to the next page                        |
| Z or <PageUp> | <page-up>        | go to the previous page                    |
| = or <Home>   | <first-entry>    | jump to the first entry                    |
| * or <End>    | <last-entry>     | jump to the last entry                     |
| q             | <quit>           | exit the current menu                      |
| ?             | <help>           | list all key bindings for the current menu |

**Most common navigation keys in page-based menus**

| Key                    | Function        | Description               |
| J or <Return>          | <next-line>     | scroll down one line      |
| <Backspace>            | <previous-line> | scroll up one line        |
| <Space> or <PageDn> | <next-page>     | move to the next page     |
| - or <PageUp>          | <previous-page> | move to the previous page |
| <Home>                 | <top>           | move to the top           |
| <End>                  | <bottom>        | move to the bottom        |

## Editing Input fields
### Introduction line editor
Mutt has a built-in line editor for inputting text, e.g. email addresses or filenames. The keys used to manipulate text input are very similar to those of Emacs.

**Most common line editor keys**

| Key            | Function           | Description                          |
| ^A or <Home>   | <bol>              | move to the start of the line        |
| ^B or <Left>   | <backward-char>    | move back one char                   |
| Esc B          | <backward-word>    | move back one word                   |
| ^D or <Delete> | <delete-char>      | delete the char under the cursor     |
| ^E or <End>    | <eol>              | move to the end of the line          |
| ^F or <Right>  | <forward-char>     | move forward one char                |
| Esc F          | <forward-word>     | move forward one word                |
| <Tab>          | <complete>         | complete filename or alias           |
| ^T             | <complete-query>   | complete address with query          |
| ^K             | <kill-eol>         | delete to the end of the line        |
| Esc d          | <kill-eow>         | delete to the end of the line        |
| ^W             | <kill-word>        | delete to the end of the word        |
| ^U             | <kill-line>        | delete entire line                   |
| ^V             | <quote-char>       | quote the next typed key             |
| <Up>           | <history-up>       | recall previous string from history  |
| <Down>         | <history-down>     | recall next string from history      |
| <Backspace>    | <backspace>        | kill the char in front of the cursor |
| Esc u          | <upcase-word>      | convert word to upper case           |
| Esc l          | <downcase-word>    | convert word to lower case           |
| Esc c          | <captitalize-word> | capitalize the word                  |
| ^G             | n/a                | abort                                |
| <Return>       | n/a                | finish editing                       |

### History
Mutt maintains a history for the built-in editor. The number of items is controlled by the `$history` variable and can be made persistent using and external file specified using `$history_file`.

Mutt maintains several distinct history lists:
- .muttrc commands
- addresses and aliases
- shell commands
- filenames
- patterns
- everything else

Mutt automatically filters out consecutively repeated items from the history. It also mimics the behavior of some shells by ignoring items starting with a space.

## Reading Mail

## Sending Mail

## Forwarding and Bouncing Mail

## Postponing Mail

# Configuration
`~/.mutt/muttrc`

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
Create a pair of public/private keys: `gpg --gen-key`

Create a file in a secure environment since it will contain your passwords for a couple of seconds: `~/.my-pwds`

	set my_pw_personal = "first password"
	set my_pw_work = "second password"

>**Note:** Remember that user defined variables must start with `my_`.

Now encrypt the file: `gpg -e -r 'your name' ~/.my-pwds`

>**Note:** 'your-name' must match the one you provided at the `gpg --gen-key` step. Now you can wipe your file containing your passwords in clear: `shred -xu ~/.my-pwds`

Back to your account dedicated files, e.g. `.mutt/muttrc`:

	set imap_pass=$my_pw_personal
	# Every time the password is needed, use $my_pw_personal variable.

And in your `.muttrc`, before you source any account dedicated file: `source "gpg2 -dq $HOME/.my-pwds.gpg |"`

>**Note:** At the end of the line above, there is no space between the pipe and the double quote.

- The `-q` parameter makes gpg2 quiet which prevents gpg2 output messing with Mutt interface.
- The pipe `|` at the end of a string is the Mutt syntax to tell that you want the result of what is preceding.

When Mutt starts, it will first source the result of the password decryption, that's why it will prompt for a passphrase. Then all passwords will be stored in memory in specific variables for the time Mutt runs. Then, when a folder-hook is called, it sets the `imap_pass` variable to the variable holding the appropriate password. When switching accounts, the `imap_pass` variable will be set to another variable holding another password, etc.

## Security concern
If `enter-command` is available from the UI, it is possible to see the password unencrypted, which may be undesired if anybody else than you has access to your session while Mutt is running. You may want to disable it for this reason. As a consequence, every command that the user intends to use must be bound to a key in advance, otherwise it will never be accessible.

	.muttrc
	bind generic,alias,attach,browser,editor,index,compose,pgp,pager,postpone ':' noop

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

# Mutt's MIME support

# Optional Features

# Security Considerations

# Performance Tuning

# References
- [Manual References](http://www.mutt.org/doc/manual/#reference)
