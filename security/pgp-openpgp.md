[TOC]

# Overview
**Pretty Good Privacy (PGP)** is *data encryption and decryption* software that provides *cryptographic privacy* and *authentication* for data communication.

PGP is often used for signing, encrypting, and decrypting texts, e-mails, files, directories, and whole disk partitions and to increase the security of e-mail communications.

## History
- Phil Zimmermann created the first version of PGP encryption in 1991.
- In July 1997, PGP Inc. proposed to the IETF that there be a standard called OpenPGP.
	+ The current specification is [RFC 4880][3] (November 2007)
	+ In 2012, encryption based on elliptic curve cryptography (ECDSA, ECDH) was extended by [RFC 6637][4]
	+ Support of EdDSA will be added by [draft-koch-eddsa-for-openpgp-00][1] proposed in 2014

# Design
PGP encryption uses a serial combination of **hashing**, **data compression**, **symmetric-key cryptography**, and finally **public-key cryptography**; each step uses one of several supported algorithms.

The first version of this system was generally known as a **web of trust** to contrast with the **X.509 system**. Current versions of PGP encryption include both options through an automated key management server.

## Compatibility
Newer PGP systems that support newer features and algorithms are able to create encrypted messages that older PGP systems cannot decrypt, even with a valid private key. Therefore, it is essential that partners in PGP communication understand the PGP system of each other.

# References
- [Homepage][1]
- [Wikipedia][2]
- [RFC4880 - OpenPGP][3]
- [RFC6637 - ECDSA/ECDH][4]
- [EdDSA Draft][5]

[1]: http://www.openpgp.org/ "OpenPGP Homepage"
[2]: https://en.wikipedia.org/wiki/Pretty_Good_Privacy "Wikipedia Pretty Good Privacy"
[3]: https://tools.ietf.org/html/rfc4880 "RFC 4880"
[4]: https://tools.ietf.org/html/rfc6637 "RFC 6637"
[5]: https://tools.ietf.org/html/draft-koch-eddsa-for-openpgp-00 "EdDSA Draft"
