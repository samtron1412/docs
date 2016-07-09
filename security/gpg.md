[TOC]

# Overview
GNU Privacy Guard (GnuPG or GPG) is a free software replacement for Symantec's PGP cryptographic software suite. GnuPG is compliant with RFC 4880.

The GnuPG 1.x series uses an integrated cryptographic library, while the GnuPG 2.x series replaces this with libgcrypt.

By default, GnuPG uses the CAST5 symmetrical algorithm. GnuPG does not use patented or otherwise restricted software or algorithms. Instead, GnuPG uses a variety of other, non-patented algorithms.

## History
- GnuPG was initially developed by Werner Koch.
- Version 1.0.0, which was the first production version, was released on September 7, 1999, almost two years after the first GnuPG release (version 0.0.0).
- The German Federal Ministry of Economics and Technology funded the documentation and the port to Microsoft Windows in 2000.
- As of November 2014, there are three actively maintained branches of GnuPG:
	+ **Stable** (2.0): stable version for general use, initially released on November 13, 2006.
	+ **Modern** (2.1): containing the latest development with numerous new features such as elliptic curve cryptography; It was initially released on November 6, 2014.
	+ **Classic** (1.4): older standalone version, most suitable for older or embedded platforms. Initially released on December 16, 2004.
	+ Stable and Modern cannot be installed at the same time. However, it is possible to install classic along with any modern or stable version.

## Limitations
- GnuPG 1.x is not written as an API that may be incorporated into other software. To overcome this, GPGME (GnuPG Make Easy) was created as an API wrapper around GnuPG that parses the output of GnuPG and provides a stable and maintainable API between the components.
- Since GnuPG 2.0, many of GnuPG's functions are available directly as C APIs in libgcrypt.

# libgcrypt
Libgcrypt is a cryptographic library (written in C) developed as a separated module of GnuPG. It can also be used independently of GnuPG, but depends on its error-reporting library.

# Basic Usage
- To generate a key: `$ gpg --full-gen-key`
- View all keys: `$ gpg --list-keys`
- View the key id
	+ Short form: `$ gpg --keyid-format short --list-keys`
	+ Long form: `$ gpg --keyid-format long --list-keys`
- Verify a signature: `$ gpg --verify doc.sig`
- Manually import a public key: `$ gpg --import public.key`
- Edit a key: `$ gpg --edit-key your@email.com/your-key-id`
	+ `gpg> adduid`: add new user id for this key

## Using a keyserver
You can register your key with a public PGP key server, so that others can retrieve your key without having to contact you directly.

Most keyservers synchronize with each other, so there is generally no need to send keys to more than one server. The keyserver **hkp://keys.gnupg.net** uses **round robin DNS** to give a different keyserver each time you use it.

Default keyserver set in `dirmngr.conf`

+ Send keys: `$ gpg --send-keys <key-id>`
+ Search keys: `$ gpg --search-keys <key-id>`
+ Import a key from a key server: `$ gpg --recv-keys <key-id>`
+ Automatically fetch keys from key servers: adding `keyserver-options auto-key-retrieve` to `gpg.conf`

# Best practices
- In general, one key per identity. If you want to manage multiple IDs which shall not be connected directly: a personal one, one at you employer, one for stuff which may not contain your real information.
- One key can include
	+ Several UIDs (for separating mail addresses, names, etc): use `--edit-key` and `adduid`
	+ Several subkeys (for diffrent devices): `--edit-key` and `addkey`

# References
- [Homepage](https://www.gnupg.org/)
- [Wikipedia](https://en.wikipedia.org/wiki/GNU_Privacy_Guard)
- [libgcrypt - Wikipedia](https://en.wikipedia.org/wiki/Libgcrypt)
