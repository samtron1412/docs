[TOC]

# [Overview](http://svnbook.red-bean.com/nightly/en/index.html)
CollabNet founded the Subversion project in 2000.

# SVN tutorial
## SVN architecture
<figure>
  <figcaption style="text-align:center;">SVN architecture</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="subversion/svn-arch-diagram.png" alt="SVN architecture" title="SVN architecture">
</figure>

## SVN's components
**svn**
The command-line client program

**svnversion**
A program for reporting the state (in terms of revisions of the items present) of a working copy

**svnlook**
A tool for directly inspecting a Subversion repository

**svnadmin**
A tool for creating, tweaking, or repairing a Subversion repository

**mod_dav_svn**
A plug-in module for the Apache HTTP Server, used to make your repository available to others over a network

**svnserve**
A custom standalone server program, runnable as a daemon process or invokable by SSH; another way to make your repository available to others over a network

**svndumpfilter**
A program for filtering Subversion repository dump streams

**svnsync**
A program for incrementally mirroring one repository to another over a network

**svnrdump**
A program for performing repository history dumps and loads over a network

**svnmucc**
A program for performing multiple repository URL-based operations in a single commit and without the use of a working copy


## Features
- Commits as true atomic operations.
- Renamed/copied/moved/removed files retain full revision history.
- Maintains versioning for directories, renames, and file metadata (but not for timestamps.)
- Versioning of symbolic links.
- Native support for binary files, with space-efficient binary-diff storage.
- Branching is a cheap operation.
- Merge tracking - Merges between branches will be tracked, this allows automatically merging between branches without telling Subversion what (doesn't) need to be merged.

## Layers
**File system**: FSFS lowest level, stores the user data.

**Repos** has many helper functions and handles the various "hooks" that a repository may have.

**mod_dav_svn** provides WebDAV/Delta-V access through Apache 2.

**Ra** Handles "repository access", both local and remote. From this point on, repositories are referred to using URLs, e.g.

**Client** the highest level. It abstracts repository access and provides common client tasks, such as authenticating users or comparing versions. Subversion clients use the **Wc** library to manage the local working copy.

# SVN workflows

# SVN clients
## TortoiseSVN
### Graph
Draw graph of project.

### Show log
Show log commit to newest commit.

### Repository browser
Browser repository.

### Check for modification
Check files is modified and create new non-versioned.

### Tortoise Merge
- diff
- resolve conflict
- applying patch files

### Tortoise Diff

### Tortoise Blame
View files with more information who commit which line of code and more info to debug.




# SVN config
## Authentication
### httpd
file subversion.conf in /etc/httpd/conf.d/

```
# Make sure you uncomment the following if they are commented out
LoadModule dav_svn_module     modules/mod_dav_svn.so
LoadModule authz_svn_module   modules/mod_authz_svn.so

# Add the following to allow a basic authentication and point Apache to where the actual
# repository resides.
<Location /repos>
        DAV svn
        SVNPath /var/www/svn/repos
        AuthType Basic
        AuthName "Subversion repos"
        AuthUserFile /etc/svn-auth-conf
        Require valid-user
</Location>
```

### Build-in authentication
svnserve

http://svnbook.red-bean.com/en/1.7/svn.serverconfig.svnserve.html#svn.serverconfig.svnserve.auth

### svn + ssh

http://svnbook.red-bean.com/en/1.7/svn.serverconfig.svnserve.html#svn.serverconfig.svnserve.sshtricks.fixedcmd