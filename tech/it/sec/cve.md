[TOC]

# Overview

- The Common Vulnerabilities and Exposures (CVE) system provides a reference-method for publicly known information security vulnerabilities and exposures.
- The **National Cybersecurity FFRDC**, operated by the **MITRE Corporation**, maintains the system, with funding from the **National Cyber Security Division** of the **United States Department of Homeland Security**.
- CVE IDs are listed on MITRE's system as well as in the US **National Vulnerability Database**.
- Requesting a CVE ID: using the [CVE Request Form][4]

# CVE identifiers

- MITRE Corporation's documentation defines CVE Identifiers as unique, common identifiers for publicly known information-security vulnerabilities in publicly released software packages.
- The assignment of a CVE identifier is not a guarantee that it will become an official CVE entry (e.g. a CVE may be improperly assigned to an issue which is not a security vulnerability, or which duplicates and existing entry).
- CVEs are assigned by a CVE Numbering Authority (CNA); there are three primary types of CNA:
	+ The MITRE Corporation functions as Editor and Primary CNA.
	+ Various CNAs assign CVE numbers for their own products (e.g. Microsoft, Oracle, HP, Red Hat, etc.)
	+ A third party coordinator such as CERT Coordination Center may assign CVE numbers for products not covered by other CNAs.
- CVE numbers may not appear in the MITRE or NVD CVE databases for some time due to issues that are embargoed (the CVE number has been assigned but the issues has not been made public), or in cases where the entry is not researched and written up by MITRE due to resource issues.

# CVE data fields

- **Description**: This is a standardized text description of the issue(s). One common entry is: `** RESERVED ** This candidate has been reserved by an organization or individual that will use it when announcing a new security problem. When the candidate has been publicized, the details for this candidate will be provided.` This means that the entry number has been reserved by MITRE for an issue or a CNA has reserved the number.
- **References**: This is a list of URLs and other information (such as vendor advisory numbers) for this issue.
- **Date Entry Created**: This is the date the entry was created. It's not the date when this issue was discovered.

# Famous CVEs

1. [heartbleed][2]
2. [shellshock][3]

## Efail

- [efail][5]

### Thoughts about this bug

```
My thoughts about Efail are a bit more nuanced.

First off, the real story here is the insecurity of S/MIME. That
protocol is used by a huge number of firms handling confidential and
classified email. The fact that this protocol — and Microsoft Outlook —
are broken is a really big deal. There have been several breaches of
defense contractors here in the US, and I’m sure that similar hacks have
occurred in Europe. It’s a very big problem that our “main” corporate
encrypted email protocol is this weak.

Regarding PGP:

In general, I think it’s much more useful to look at the overall
security of a system, rather than trying to assign blame to different
components. The PGP “community”, by which I mean a collection of open
source developers on GnuPG and other client projects, have spent a lot
of time trying to assign blame. This isn’t very interesting to me.

The fact of the matter is that Efail is a very serious bug that occurs
across a large number of different email clients. It enables total
decryption of email messages, something that absolutely should not be
possible in 2018. Even worse, the flaws that cause Efail have been well
known since at least 2000-2001. The fact that this is occurring in so
many different email clients indicates, to me, that the PGP tool
development community is not pursuing cryptographic security to the
extent required of a serious encryption tool.

Rather than ask “who to blame”, I’d say: ask *why* this is occurring.

The answer, it seems to me, is that nobody is really *leading* the PGP
community in any way. Leadership in this sense means somebody who is in
a position of influence, who works on various projects, and who uses and
communicates with other developers in the space. This person would be
aware when clients are doing things improperly, and would say something
about it. If possible they would modify their own tools to ensure that
third party clients can’t misuse them. Other open source encryption
projects like TLS have the IETF and a handful of strong experts in
corporate positions. PGP doesn’t really have anything comparable.

A natural location for this kind of leadership would be the GnuPG
project, which is a tool that most of these systems use. But the
managers of the GnuPG project have mostly decided that this is somebody
else’s problem. And they’ve made that clear in the way they responded to
Efail.

In the absence of clear security leadership, my view is: take very good
care using this ecosystem. Because unless you’ve extensively reviewed
all of the tools that you’re using, you can’t be sure that they will
interact safely together, since nobody else is checking their work. And
even if *you* get everything right, you’re not safe unless you make sure
that all of your communication partners are also using safe toolchains.
In my opinion, this is very hard to get right. And so — until this
changes substantially -- I wouldn’t trust the PGP ecosystem for
extremely sensitive communications.
```

- https://neopg.io/blog/efail/
- https://efail.de/efail-attack-paper.pdf

# References

1. [Wikipedia - Common Vulnerabilities and Exposures][1]
2. [Wikipedia - Heartbleed][2]
3. [Wikipedia - Shellshock][3]
4. [CVE Request Form][4]

[1]: https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures "Wikipedia - Common Vulnerabilities and Exposures"
[2]: https://en.wikipedia.org/wiki/Heartbleed "Wikipedia - Heartbleed"
[3]: https://en.wikipedia.org/wiki/Shellshock_(software_bug) "Wikipedia - Shellshock"
[4]: https://cveform.mitre.org/ "CVE Request Form"
[5]: https://efail.de/
