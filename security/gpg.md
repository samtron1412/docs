[TOC]

# Overview
- [Homepage](https://www.gnupg.org/)
- [Wikipedia](https://en.wikipedia.org/wiki/GNU_Privacy_Guard)

# Basic Usage
- To generate a key: `$ gpg --full-gen-key`
- View all keys: `$ gpg --list-keys`
- View the key id
	+ Short form: `$ gpg --keyid-format short --list-keys`
	+ Long form: `$ gpg --keyid-format long --list-keys`
- Verify a signature: `$ gpg --verify doc.sig`

## Using a keyserver
You can register your key with a public PGP key server, so that others can retrieve your key without having to contact you directly.

Most keyservers synchronize with each other, so there is generally no need to send keys to more than one server. The keyserver **hkp://keys.gnupg.net** uses **round robin DNS** to give a different keyserver each time you use it.

Default keyserver set in `dirmngr.conf`

+ Send keys: `$ gpg --send-keys <key-id>`
+ Search keys: `$ gpg --search-keys <key-id>`
+ Import a key from a key server: `$ gpg --recv-keys <key-id>`
+ Automatically fetch keys from key servers: adding `keyserver-options auto-key-retrieve` to `gpg.conf`
