[TOC]

# Overview
In Engineer view, we need experience and compare between products to choose right product at each specific conditions.

# Web development
## [Active Record vs Data Mapper](http://culttt.com/2014/06/18/whats-difference-active-record-data-mapper/)

## [Doctrine 2 vs Eloquent](http://culttt.com/2014/07/07/doctrine-2-different-eloquent/)

## [nginx vs apache](https://www.digitalocean.com/community/tutorials/apache-vs-nginx-practical-considerations#distributed-vs-centralized-configuration)
### General
- **Apache** is often chosen by administrators for its flexibility, power, and widespread support. It is extensible through a dynamically loadable module system and can process a large number of interpreted languages without connecting out to separate software.
- **Nginx** is often selected by administrators for its resource efficiency and responsiveness under load.

### Connection Handling Architecture
- **Apache** provides a variety of multi-processing modules (Apache calls these MPMs) that dictate how client requests are handled.
	+ **mpm_prefork** : process
	+ **mpm_worker** : threaded
	+ **mpm_event** : event handle like Nginx, stable with Apache 2.4
- **Nginx** was designed from the ground up to use an *asynchronous*, *non-blocking*, *event-driven* connection handling algorithm.

### Static vs Dynamic content
- Rather than using the *embedded interpreter* approach, Nginx hands off dynamic content to *CGI, FastCGI, or even other web severs like Apache*, which is then passed back to Nginx for delivery to the client.
- **Nginx** does not have any ability to process dynamic content natively. To handle PHP and other requests for dynamic content, Nginx must pass to an external processor for execution and wait for the rendered content to be sent back. The results can then be relayed to the client. **Apache** can also process dynamic content by embedding a processor of the language in question into each of its worker instances.

### Distributed vs Centralized Configuration


### File vs URI-Based Interpretation


### Modules


### Support, Compatibility, Ecosystem, and Documentation


### Using Apache and Nginx Together

# Editor - IDE
## vim vs Emacs
- http://unix.stackexchange.com/questions/986/what-are-the-pros-and-cons-of-vim-and-emacs
-


# Toyota vs Honda vs Hyundai
Toyota is the most popular.

Honda is the next.

# Certification vs Diploma vs Degree
## Certification
Certification programs are specialized and industry specific. These programs don't offer a broad overview of a field or industry, and are often a good option for someone who already has a degree or work experience in the field.

## Diploma
Diploma programs are specialized but more in depth than certification programs. Diplomas are also what you receive upon graduating high school.

## Degree
Degree programs are awarded by colleges and universities. A degree program is often requires the student o take general education courses to support a more rounded education.
	+ An **associate's degree** is two-year degree most commonly granted by a community college or technical school. They can also be granted by four-year colleges and universities.
	+ A **bachelor's degree** is a four-year degree that is granted by a college or university.
	+ A **master's degree** is what is called a post-graduate degree because you go on to get one only after you have graduated with your bachelor's.
	+ A **Ph.D** is another example or a post-graduate degree, and is several more years of study and intensive research.

# Thesis vs Dissertation
The differences between a thesis and a dissertation it really depends upon the requirements set forth by each specific school or academic program. Most universities make their dissertation/thesis guidelines available online so it's best to view them ahead of time so you aware of what will be required of you.

In USA
1. A thesis is submitted **at the end of one's master's degree**, and a dissertation is submitted **at the end of a PhD**.
2. For a thesis, you have **conduct original research**, while for a dissertation you have to **synthesize already existing literature**.
3. Thesis analysis **is added to the already existing literature**, while dissertation is **an analysis of the existing literature**.

# Grill, Broil, Toast, Roast and Bake
- **GRILL**: heat from below, usually fairly hot...it's generally food that's placed on the grill rack of an outdoor grill, or on one of the new "grill pans" on a stove top (however, an outdoor grill can also be made into more of an "oven" by closing its lid, or just putting the food over an area of the grill's rack that's not directly over coals or fire)
- **BROIL**: The heat comes from the top to cook the food.
- **TOAST**: Generally the heat is both top and bottom (or side to side in a toaster) and it is a dry cooking method with a food that has little moisture, bread for example
- **ROAST**: Higher temperature with the intent to caramelize the outer portion of the food to bring out flavor. An example of this would be roasting a piece of meat, or vegetables. The pan is large enough to allow heat to reach most sides of the food that is being cooked.
- **BAKE**: In the case of cakes or casseroles the food fills the pan so that you get even cooking but the food does not dry out. Also used as a general term for cooking almost anything in the oven.

# PGP - OpenPGP - GnuPG vs SSH - OpenSSH
- **OpenPGP** is a standard for data encryption and decryption.
- **PGP(Pretty Good Privacy)** is a data encryption and decryption computer program that provides cryptographic privacy and authentication for data communication. PGP follows the OpenPGP standard.
- **GnuPG(GNU Privacy Guard)** is a free software replacement for Symantec's PGP cryptographic software suite. GnuPG implements OpenPGP standard.
- **SSH** is a network protocol for secure data communication and remote command execution
- **OpenSSH** is a suite of security-related network-level utilities based on the SSH protocol.

## Comparing GPG keys and SSH keys
- Client SSH keys are used to authenticate who you are to a server. (The SSH server also has its own pair of keys it uses to authenticate who it is to the clients.)
- GPG keys are used to authenticate a message with a digital signature, or to act as a key for decrypting messages to you.

# syslog-ng, rsyslog, journald
- https://bazsi.blogs.balabit.com/2011/12/syslog-ng-and-the-journal/
- http://blog.gerhards.net/2013/05/rsyslog-vs-systemd-journal.html

# Git Merge vs Rebase
In general the way to get the best of both worlds is to rebase local changes you’ve made but haven’t shared yet before you push them in order to clean up your story, but never rebase anything you’ve pushed somewhere.

## Merge
create new commit and merge two ancestor commits. hold all history of commit

## Rebase
replay all commit of one branch to another branch and clean history of commit. clean history commit. should use locally, not rebase anything you pushed somewhere.
