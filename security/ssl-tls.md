[TOC]

# Overview


# Opportunistic TLS (STARTTLS)
Opportunistic TLS refers to extensions in plain text communication protocols, which offer a way to upgrade a plain text connection to an encrypted (TLS or SSL) connection instead of using a separate port for encrypted communication. Several protocols use a command named "STARTTLS" for this purpose.

The STARTTLS command for **IMAP** and **POP3** is defined in [RFC 2595](https://tools.ietf.org/html/rfc2595), for **SMTP** in [RFC 3207](https://tools.ietf.org/html/rfc3207), for **XMPP** in [RFC 6120](https://tools.ietf.org/html/rfc6120) and for **NNTP** in [RFC 4642](https://tools.ietf.org/html/rfc4642). For **IRC**, the de facto definition is documented at the [InspIRCd Wiki](https://wiki.inspircd.org/STARTTLS_Documentation). **FTP** uses the command "AUTH TLS" defined in [RFC 4217](https://tools.ietf.org/html/rfc4217) and **LDAP** defines a protocol extension **OID** in [RFC 2830](https://tools.ietf.org/html/rfc2830).
