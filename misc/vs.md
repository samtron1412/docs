[TOC]

# Overview

An engineer has to experience and compare things in order to choose
a right solution in specific conditions.

# Thread vs Process

## Introduction

- The process model is based on two independent concepts:
    + **resource grouping** (processes)
    + **execution** (threads)

## Process

- Each process provides the resources needed to execute program
    + It is a way to group related resources together
- A process has
    + A virtual address space stores text and data
    + signals and signal handlers
    + A security context
    + A unique process identifier
    + environment variables
    + A priority class
    + minimum and maximum working set sizes
    + Open files
    + Child processes
    + At least one **thread of execution**
    + etc.

## Thread

- A thread is an entity within a process that can be scheduled for
  execution
    + thread of execution
- All threads of a process share its virtual address space and system
  resources. In addition,
    + a program counter (pc) that keeps track of which instruction to
      execute next
    + each thread maintains exception handlers
    + a scheduling priority
    + thread local storage
    + a unique thread identifier
    + a set of structures the system will use to save the thread context
      until it is scheduled. The thread context includes
        * the thread's set of machine registers
        * the kernel stack
        * a thread environment block
        * a user stack in the address space of the thread's process
    + threads can also have their own security context, which can be
      used for impersonating clients
- Software threads
    + User-space threads
        * switching is fast
        * can't block I/O
    + Kernel threads
        * a little slower
        * can block I/O
    + A combination of the two

## Benefits of separated concepts

- Programming abstraction
    + Dividing up work and assigning each division to a unit of
      execution (a thread) is a natural approach to many problems
    + Programming patterns: reactor, thread-per-connection, and thread
      pool
    + Alan Cox: "threads are for people who can't program state
      machines"
- Parallelism
    + In machine with multiple processors, threads provide an efficient
      way to achieve true parallelism.
    + Each thread receives its own virtualized processor and is an
      independently-schedulable entity, multiple threads may run on
      multiple processors at the same time, improving a system's
      throughput.
    + To the extent that threads are used to achieve parallelism, that
      is, there are no more threads than processors => The Alan Cox's
      quote does not apply.
- Blocking I/O
    + Without threads, blocking I/O halts the whole process => this can
      be detrimental (damaging) to both throughput and latency.
    + In a multithreaded process, individual threads may block, waiting
      on I/O, while other threads make forward progress.
    + *Asynchronous and non-blocking I/O* are alternative solutions to
      threads for this issue.
- Memory savings
    + Threads provide an efficient way to share memory yet utilize
      multiple units of execution => in this manner they are an
      alternative to multiple processes.

## Funny stuff

- Why doesn't Windows 95 format floppy disks smoothly?
    + https://blogs.msdn.microsoft.com/oldnewthing/20090102-00/?p=19623/

# GPT vs MBR

- https://www.techlila.com/mbr-vs-gpt/
- https://www.howtogeek.com/193669/whats-the-difference-between-gpt-and-mbr-when-partitioning-a-drive/
- https://en.wikipedia.org/wiki/GUID_Partition_Table

# BIOS vs UEFI

- https://superuser.com/questions/496026/what-is-the-difference-in-boot-with-bios-and-boot-with-uefi#501867

# AHCI mode vs IDE mode vs RAID mode

- https://answers.microsoft.com/en-us/windows/forum/windows_8-hardware/what-does-ahci-mode-ide-mode-raid-mode-sata-mean/d622d5cd-41c4-4b84-90ef-cea69aa47089

# Web development

## [Active Record vs Data Mapper](http://culttt.com/2014/06/18/whats-difference-active-record-data-mapper/)

## [Doctrine 2 vs Eloquent](http://culttt.com/2014/07/07/doctrine-2-different-eloquent/)

## [nginx vs apache](https://www.digitalocean.com/community/tutorials/apache-vs-nginx-practical-considerations#distributed-vs-centralized-configuration)

### General

- **Apache** is often chosen by administrators for its flexibility,
  power, and widespread support. It is extensible through a dynamically
  loadable module system and can process a large number of interpreted
  languages without connecting out to separate software.
- **Nginx** is often selected by administrators for its resource
  efficiency and responsiveness under load.

### Connection Handling Architecture

- **Apache** provides a variety of multi-processing modules (Apache
  calls these MPMs) that dictate how client requests are handled.
    + **mpm_prefork** : process
    + **mpm_worker** : threaded
    + **mpm_event** : event handle like Nginx, stable with Apache 2.4
- **Nginx** was designed from the ground up to use an *asynchronous*,
  *non-blocking*, *event-driven* connection handling algorithm.

### Static vs Dynamic content

- Rather than using the *embedded interpreter* approach, Nginx hands off
  dynamic content to *CGI, FastCGI, or even other web severs like
  Apache*, which is then passed back to Nginx for delivery to the
  client.
- **Nginx** does not have any ability to process dynamic content
  natively. To handle PHP and other requests for dynamic content, Nginx
  must pass to an external processor for execution and wait for the
  rendered content to be sent back. The results can then be relayed to
  the client. **Apache** can also process dynamic content by embedding a
  processor of the language in question into each of its worker
  instances.

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

Certification programs are specialized and industry specific. These
programs don't offer a broad overview of a field or industry, and are
often a good option for someone who already has a degree or work
experience in the field.

## Diploma

Diploma programs are specialized but more in depth than certification
programs. Diplomas are also what you receive upon graduating high
school.

## Degree

Degree programs are awarded by colleges and universities. A degree
program is often requires the student o take general education courses
to support a more rounded education.
    + An **associate's degree** is two-year degree most commonly granted
      by a community college or technical school. They can also be
      granted by four-year colleges and universities.
    + A **bachelor's degree** is a four-year degree that is granted by a
      college or university.
    + A **master's degree** is what is called a post-graduate degree
      because you go on to get one only after you have graduated with
      your bachelor's.
    + A **Ph.D** is another example or a post-graduate degree, and is
      several more years of study and intensive research.

# Thesis vs Dissertation

The differences between a thesis and a dissertation it really depends
upon the requirements set forth by each specific school or academic
program. Most universities make their dissertation/thesis guidelines
available online so it's best to view them ahead of time so you aware of
what will be required of you.

In USA
1. A thesis is submitted **at the end of one's master's degree**, and a
   dissertation is submitted **at the end of a PhD**.
2. For a thesis, you have **conduct original research**, while for a
   dissertation you have to **synthesize already existing literature**.
3. Thesis analysis **is added to the already existing literature**,
   while dissertation is **an analysis of the existing literature**.

# Grill, Broil, Toast, Roast and Bake

- **GRILL**: heat from below, usually fairly hot...it's generally food
  that's placed on the grill rack of an outdoor grill, or on one of the
  new "grill pans" on a stove top (however, an outdoor grill can also be
  made into more of an "oven" by closing its lid, or just putting the
  food over an area of the grill's rack that's not directly over coals
  or fire)
- **BROIL**: The heat comes from the top to cook the food.
- **TOAST**: Generally the heat is both top and bottom (or side to side
  in a toaster) and it is a dry cooking method with a food that has
  little moisture, bread for example
- **ROAST**: Higher temperature with the intent to caramelize the outer
  portion of the food to bring out flavor. An example of this would be
  roasting a piece of meat, or vegetables. The pan is large enough to
  allow heat to reach most sides of the food that is being cooked.
- **BAKE**: In the case of cakes or casseroles the food fills the pan so
  that you get even cooking but the food does not dry out. Also used as
  a general term for cooking almost anything in the oven.

# PGP - OpenPGP - GnuPG vs SSH - OpenSSH

- **OpenPGP** is a standard for data encryption and decryption.
- **PGP(Pretty Good Privacy)** is a data encryption and decryption
  computer program that provides cryptographic privacy and
  authentication for data communication. PGP follows the OpenPGP
  standard.
- **GnuPG(GNU Privacy Guard)** is a free software replacement for
  Symantec's PGP cryptographic software suite. GnuPG implements OpenPGP
  standard.
- **SSH** is a network protocol for secure data communication and remote
  command execution
- **OpenSSH** is a suite of security-related network-level utilities
  based on the SSH protocol.

## Comparing GPG keys and SSH keys

- Client SSH keys are used to authenticate who you are to a server. (The
  SSH server also has its own pair of keys it uses to authenticate who
  it is to the clients.)
- GPG keys are used to authenticate a message with a digital signature,
  or to act as a key for decrypting messages to you.

# syslog-ng, rsyslog, journald

- https://bazsi.blogs.balabit.com/2011/12/syslog-ng-and-the-journal/
- http://blog.gerhards.net/2013/05/rsyslog-vs-systemd-journal.html

# Git Merge vs Rebase

In general the way to get the best of both worlds is to rebase local
changes you’ve made but haven’t shared yet before you push them in order
to clean up your story, but never rebase anything you’ve pushed
somewhere.

## Merge

create new commit and merge two ancestor commits. hold all history of
commit

## Rebase

replay all commit of one branch to another branch and clean history of
commit. clean history commit. should use locally, not rebase anything
you pushed somewhere.

# git-am, git-apply, git-diff, git-format-patch

- When patches are in `git-diff` format then should use `git-apply` to
  apply patches. You can modify after apply these patches and commit
  them like a new commit.
- When patches are in `git-format-diff` format then should use `git-am`
  to apply patches, it will create commits in repository.

# Perforce (central version control system), git, mercurial

- Perforce use for very large projects (>6GB)
- Git, Mercurial use for smaller projects.

# Virtual Private Network (VPN) vs Tor

- [security.stackexchange][1]
- [Using VPN and Tor together][2]

[1]: https://security.stackexchange.com/questions/72679/differences-between-using-tor-browser-and-vpn "Tor and VPN"
[2]: https://www.bestvpn.com/blog/42672/using-vpn-and-tor-together/ "Using VPN and Tor together"

# RDP vs RFB (VNC)

- [What's the difference between RDP vs RFB(VNC)][1]
    + RFB: sending the actual images across the network.
    + RDP: sending the information how to draw the images. So RDP a lot
      faster than RFB in most cases.

[1]: http://superuser.com/questions/32495/whats-the-difference-between-rdp-vs-vnc "What's the difference between RDP vs RFB(VNC)"

# GNU Screen, tmux, byobu

- [Byobu vs. GNU Screen vs. tmux - usefulness and transferability of skills][1]
    + byobu is a configuration platform build on top of GNU Screen and
      tmux. So GNU Screen and tmux are backend of byobu.

[1]: http://superuser.com/questions/423310/byobu-vs-gnu-screen-vs-tmux-usefulness-and-transferability-of-skills "Byobu vs. GNU Screen vs. tmux -- usefulness and tranferability of skills"

# directory vs folder

- `folder`: is referring to a container of files, folders. It is a
logical term. Using it to refer a place to store things. For example,
Packages folder.
- `directory`: refers to the way a structured list of document files and
folders is stored on the computer. Using it when you see an absolute
path. For example, `/usr/bin/` directory.

# simulator/simulation/simulate vs emulator/emulation/emulate

- Emulation is the process of mimicking the outwardly observable
behavior to match an existing target.
    + The internal state of the emulation mechanism does not have to
    accurately reflect the internal state of the target which is
    emulating.
    + An emulation can replace the original for `real` use.
- Simulation involves modeling the underlying state of the target.
    + A simulator is a model for analysis.

# Microcontroller vs. Microprocessor

| Attributes        | Microcontroller                                                                                  | Microprocessor                                                  |
| -                 | -                                                                                                | -                                                               |
| Application       | Specific and are designed to perform certain limited tasks                                       | Generic and are capable of executing big and complicated tasks. |
| One  Solution     | Have inbuilt processor, memory, and I/O ports like a small stand-alone computer on a single chip | Generally don't have inbuilt memory and I/O ports               |
| Performance       | Limited                                                                                          | Very high                                                       |
| Speed             | Generally from 8 MHz - 200 MHz                                                                   | Generally above 1 GHz                                           |
| Power consumption | Are designed to consume less power                                                               | Consume relative more power                                     |
| Cost              | Affordable and cheap                                                                             | Very expensive and requires other peripherals                   |

# feeling vs emotion vs mood vs temperament vs personality trait

- feeling: conscious subjective experience of emotion
- emotion: conscious experience characterized by intense mental activity
  and a certain degree of pleasure or displeasure
- mood: an emotional state; in contrast to emotions, feelings, it is
  less specific, less intense and less likely to be provoked or
  instantiated by a particular stimulus or event
- temperament: refers to those aspects of an individual's personality,
  such that are often regarded as biological based (innate) rather than
  learned
- personality trait: habitual patterns of behavior, thought, and emotion
