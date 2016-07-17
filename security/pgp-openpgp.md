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

## Confidentiality
PGP can be used to send messages confidentially.
- The message is encrypted using a symmetric encryption algorithm, which requires a symmetric key.
	+ Each symmetric key is used only once and is also called a session key.
- The session key is encrypted by the receiver's public key. Only the private key belonging to the receiver can decrypt the session key.

## Digital signatures
PGP supports message authentication and integrity checking.
- **Integrity checking** is used to detect whether a message has been altered since it was completed.
- **Message authentication** is used to determine whether it was actually sent by the person or entity claimed to be the sender.
	+ PGP computes a hash (a message digest) from the plaintext and then creates the digital signature from that hash using the sender's private key.

## Web of trust
### Introduction
Both when **encrypting messages** and when **verifying signatures**, it is critical that the public key used to send messages to someone or some entity actually does **belong** to the intended recipient.

Simple downloading a public key from somewhere is not an overwhelming assurance of that association; deliberate (or accidental) impersonation is possible.

From its first version, PGP has always included provision for distributing user's public keys in an **identity certificate**, which is also constructed cryptographically so that any tempering (or accidental garble) is readily detectable.

However, merely making a certificate which is impossible to modify without being detected is insufficient; this can prevent corruption only after the certificate has been created, not before. Users must also ensure by some means that the public key in a certificate actually does belong to the person or entity claiming it.

After that version, PGP has included an **internal certificate vetting scheme** to assist with this, a trust model which has been called a web of trust.
- A given public key (information binding a user name to a key) may be digitally signed by a third party user to attest to the association between someone (actually a user name) and the key.
- There are several levels of confidence which can be included in such signatures.
- The web of trust protocol was first described by Zimmermann in 1992, in the manual for PGP version 2.0.
- Its **decentralized trust model** is an alternative to the **centralized trust model** of a public key infrastructure (PKI), which relies exclusively on a *certificate authority*.

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
