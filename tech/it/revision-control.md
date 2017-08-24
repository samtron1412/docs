[TOC]

# Overview

[Wikipedia](https://en.wikipedia.org/wiki/Revision_control)

[Category](https://en.wikipedia.org/wiki/List_of_revision_control_software)

[Comparison](https://en.wikipedia.org/wiki/Comparison_of_revision_control_software)

# Category
## Local


## Client-Server
### [Subversion](http://subversion.apache.org/)
- [Wiki](https://en.wikipedia.org/wiki/Apache_Subversion)


## Distributed
### [Git](http://git-scm.com/)
- [Wiki](https://en.wikipedia.org/wiki/Git_(software))
- Correspond with complex projects and many commiter.
- Very flexible.

#### Pros(Advantages)
- Distributed version control system. Decentralized. Your local copy is a repository, and you can commit to it and get all benefits of source control. **Offline working**. => **free to commit** not worry about breaking thing. after all you tuning thing and publish final code to everyone. => eliminate comment code, get clean code
- Git is much *faster* than Subversion: diff, view history, commit, merge, switch...
- Making *branches* and *merging* really easy.
- *Scales* to thousands of contributors.
- Use *less space*: One of the reasons for the smaller repo size is that an SVN working directory always *contains two copies of each file*: one for the user to actually work with and another hidden in .svn/ to aid operations such as status, diff and commit. In contrast a Git working directory requires only *one small index file that stores about 100 bytes of data per tracked file*. On projects with a large number of files this can be a substantial difference in the disk space required per working copy.
- Very *flexible*, many workflow.
- *Ignore* easier. ignore a pattern across all subdirectories (e.g *.txt)
- Access control
- Staging area, index (snapshot state of your files): make big modify and commit part of modify, commit part of file.

#### Cons (Disadvantages)
- Harder to learn, more concepts and more commands. Complex architecture when advanced use.
- Longer and Unpredictable revision numbers: SHA1 string

### [Mercurial](http://mercurial.selenic.com/)
- Correspond with simple projects and less commiters. (Local projects)
- Fast learn and speed (speed like git)

# Source-management models
## Atomic operations

## File locking


## Version merging


## Baselines, labels and tags
identifying a snapshot.


# Common vocabulary
Terminology can vary from system to system, but some terms in common usage include:

**Baseline**
An approved revision of a document or source file from which subsequent changes can be made. See baselines, labels and tags.

**Branch**
A set of files under version control may be branched or forked at a point in time so that, from that time forward, two copies of those files may develop at different speeds or in different ways independently of each other.

**Change**
A change (or diff, or delta) represents a specific modification to a document under version control. The granularity of the modification considered a change varies between version control systems.

**Change list**
On many version control systems with atomic multi-change commits, a change list, change set, update, or patch identifies the set of changes made in a single commit. This can also represent a sequential view of the source code, allowing the examination of source "as of" any particular changelist ID.

**Checkout**
To check out (or co) is to create a local working copy from the repository. A user may specify a specific revision or obtain the latest. The term 'checkout' can also be used as a noun to describe the working copy.

**Commit**
To commit (check in, ci or, more rarely, install, submit or record) is to write or merge the changes made in the working copy back to the repository. The terms 'commit' and 'checkin' can also be used as nouns to describe the new revision that is created as a result of committing.

**Conflict**
A conflict occurs when different parties make changes to the same document, and the system is unable to reconcile the changes. A user must resolve the conflict by combining the changes, or by selecting one change in favour of the other.

**Delta compression**
Most revision control software uses delta compression, which retains only the differences between successive versions of files. This allows for more efficient storage of many different versions of files.

**Dynamic stream**
A stream in which some or all file versions are mirrors of the parent stream's versions.

**Export**
exporting is the act of obtaining the files from the repository. It is similar to checking out except that it creates a clean directory tree without the version-control metadata used in a working copy. This is often used prior to publishing the contents, for example.

**Head**
Also sometimes called tip, this refers to the most recent commit, either to the trunk or to a branch. The trunk and each branch have their own head, though HEAD is sometimes loosely used to refer to the trunk.[7]

**Import**
importing is the act of copying a local directory tree (that is not currently a working copy) into the repository for the first time.

**Label**
See tag.
Mainline 
Similar to trunk, but there can be a mainline for each branch.

**Merge**
A merge or integration is an operation in which two sets of changes are applied to a file or set of files. Some sample scenarios are as follows:
A user, working on a set of files, updates or syncs their working copy with changes made, and checked into the repository, by other users.[8]
A user tries to check in files that have been updated by others since the files were checked out, and the revision control software automatically merges the files (typically, after prompting the user if it should proceed with the automatic merge, and in some cases only doing so if the merge can be clearly and reasonably resolved).
A set of files is branched, a problem that existed before the branching is fixed in one branch, and the fix is then merged into the other branch.
A branch is created, the code in the files is independently edited, and the updated branch is later incorporated into a single, unified trunk.

**Promote**
The act of copying file content from a less controlled location into a more controlled location. For example, from a user's workspace into a repository, or from a stream to its parent.[9]

**Repository**
The repository is where files' current and historical data are stored, often on a server. Sometimes also called a depot (for example, by SVK, AccuRev and Perforce).

**Resolve**
The act of user intervention to address a conflict between different changes to the same document.

**Reverse integration**
The process of merging different team branches into the main trunk of the versioning system.

**Revision**
Also version: A version is any change in form. In SVK, a Revision is the state at a point in time of the entire tree in the repository.

**Share**
The act of making one file or folder available in multiple branches at the same time. When a shared file is changed in one branch, it is changed in other branches.

**Stream**
A container for branched files that has a known relationship to other such containers. Streams form a hierarchy; each stream can inherit various properties (like versions, namespace, workflow rules, subscribers, etc.) from its parent stream.

**Tag**
A tag or label refers to an important snapshot in time, consistent across many files. These files at that point may all be tagged with a user-friendly, meaningful name or revision number. See baselines, labels and tags.

**Trunk**
The unique line of development that is not a branch (sometimes also called Baseline, Mainline or Master)

**Update**
An update (or sync) merges changes made in the repository (by other people, for example) into the local working copy.[8] Update is also the term used by some CM tools (CM+, PLS, SMS) for the change package concept (see changelist).

**Working copy**
The working copy is the local copy of files from a repository, at a specific time or revision. All work done to the files in a repository is initially done on a working copy, hence the name. Conceptually, it is a sandbox.

# Version naming convention
[Major version].[Minor features].[Minor bugs]-[release candidate(rc)|beta|alpha]

- alpha: the least stable
- beta: All critical dataloss and security bugs are resolved. API frozen
- release candidates (rc): nearly stable code