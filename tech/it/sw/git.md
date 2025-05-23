[TOC]

# [Overview](https://www.atlassian.com/git/)

## Basic Git Data Stores

![Git Data Stores](https://github.com/samtron1412/figures/raw/master/git/git-transport.png)

## Basic Git Workflow

![Basic Git Workflow](https://github.com/samtron1412/figures/raw/master/git/basic-git-workflow.png)

## Goals of Git

- Speed
- Simple design
- Strong support for non-linear development (thousands of parallel branches)
- Fully distributed
- Able to handle large projects like the Linux kernel efficiently (speed and data size)

## Pros (Advantages)

- Distributed version control system. Decentralized. Your local copy is
  a repository, and you can commit to it and get all benefits of source
  control. **Offline working**. => **free to commit** not worry about
  breaking thing. after all you tuning thing and publish final code to
  everyone. => eliminate comment code, get clean code
- Git is much *faster* than Subversion: diff, view history, commit, merge, switch...
- Making *branches* and *merging* really easy.
- *Scales* to thousands of contributors.
- Use *less space*: One of the reasons for the smaller repo size is that
  an SVN working directory always *contains two copies of each file*:
  one for the user to actually work with and another hidden in .svn/ to
  aid operations such as status, diff and commit. In contrast a Git
  working directory requires only *one small index file that stores
  about 100 bytes of data per tracked file*. On projects with a large
  number of files this can be a substantial difference in the disk space
  required per working copy.
- Very *flexible*, many workflow.
- *Ignore* easier. ignore a pattern across all subdirectories (e.g *.txt)
- Access control
- Staging area, index (snapshot state of your files): make big modify
  and commit part of modify, commit part of file.

## Cons (Disadvantages)

- Harder to learn, more concepts and more commands.
- Longer and Unpredictable revision numbers: SHA-1 string

## Resources

- [Git vs SVN](https://git.wiki.kernel.org/index.php/GitSvnComparsion)
- [stackoverflow](https://stackoverflow.com/questions/871/why-is-git-better-than-subversion)
- [Google talk: Linus Torvalds on git](https://www.youtube.com/watch?v=4XpnKHJAok8)
- [Google talk: Randal Schwartz - Git](https://www.youtube.com/watch?v=8dhZ9BXQgc4)
- [Introduction git with scott chacon](https://www.youtube.com/watch?v=ZDR433b0HJY)
- [Git magic](http://www-cs-students.stanford.edu/~blynn//gitmagic/)
- [Documentation](http://git-scm.com/doc)
    + [Reference Manual](http://git-scm.com/docs)
    + [Cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf)
    + [Book](http://git-scm.com/book/en/v2)
    + [External links](http://git-scm.com/documentation/external-links)
- [Blog](http://git-scm.com/blog)
- [Community](http://git-scm.com/community)
- [10 things I hate about Git](http://stevebennett.me/2012/02/24/10-things-i-hate-about-git/)
- https://www.reddit.com/r/programming/comments/xpitj/10_things_i_hate_about_git/
- https://news.ycombinator.com/item?id=4340047
- http://think-like-a-git.net/
- [My Git Workflow](http://blog.osteele.com/posts/2008/05/my-git-workflow/)


# Customizing Git

## Configuration

### Location of configuration file

- `git config --system`: apply on every user on the system and all of
  their repositories. File at `/etc/gitconfig` (Windows - it put in Git
  installation folder).
- `git config --global`: apply to specific user. File at `~/.gitconfig`
  (or ~/.config/git/config).
- `git config`: apply each repository. File in the Git directory
  (`.git/config`)

**Config in repository overrides global config and global overrides
system config.**

### Basic client configurations

**git config --global user.name "name"**

**git config --global user.email email**

**git config --global color.ui auto**

**git config --global core.editor emacs**

### Formatting and Whitespace - [Dealing with line endings](https://help.github.com/articles/dealing-with-line-endings/)

- https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings

When you see `git status` shows you some files as modified but you sure
that you had not modified that files, maybe you is victim of Line Ending
Normalization. You should run `git diff -w` command to verify what is
really changed in files, the options `-w` tells git to ignore whitespace
and line endings.

With a team with different location developers, difficult to consistent
development environment then you can turn off this feature with
`.gitattributes` files in repository: `* text=off`

>Better option is to normalize repository and turn on `autocrlf` feature
>with `.gitattributes` files.

#### Global settings for line endings

`core.autocrlf = true`: commit CRLF->LF, checkout LF->CRLF

`core.autocrlf = input`: commit CRLF->LF, checkout as-is LF

`core.autocrlf = false`: commit as-is, checkout as-is

#### Per-repository settings

Optionally, you can configure the way Git manages line endings on a per-
repository basis by configuring a special `.gitattributes` file.

This file is committed into the repository and overrides an individual's
`core.autocrlf` setting, ensuring consistent behavior for all users,
regardless of their Git settings.

The advantage of a `.gitattributes` file is that your line
configurations are associated with your repository. You don't need to
worry about whether or not collaborators have the same line ending
settings that you do.

The `.gitattributes` file must be created in the root of the repository
and committed like any other file.

```
# Set the default behavior, in case people don't have core.autocrlf set.
* text=auto

# Explicitly declare text files you want to always be normalized and converted
# to native line endings on checkout.
*.c text
*.h text

# Declare files that will always have CRLF line endings on checkout.
*.sln text eol=crlf

# Denote all files that are truly binary and should not be modified.
*.png binary
*.jpg binary
```

- `text=auto`: Git will handle the files in whatever way it thinks is
  best. This is a good default option.
- `text eol=crlf`: Git will always convert line endings to `CRLF` on
  checkout. You should use this for files that must keep `CRLF` endings,
  even on OSX or Linux.
- `text eol=lf`: Git will always convert line endings to `LF` on
  checkout. You should use this for files that must keep `LF` endings,
  even on Windows.
- `binary` Git will understand that the files specified are not text,
  and it should not try to change them. The `binary` setting is also an
  alias for `-text -diff`.

#### Refreshing a repository after changing line endings

After you've set the `core.autocrlf` option and committed a
`.gitattributes` file, you may find that Git wants to commit files that
you have not modified. At this point, git is eager to change the line
endings of every file for you.

The best way to automatically configure your repository's line endings
is to first backup your files with Git, delete every file in your
repository (except the `.git` directory), and then restore the files all
at once.

1. Save your current files in Git, so that none of your work is lost.

        $ git add . -u
        $ git commit -m "Saving files before refreshing line endings"

2. Remove every file from Git's index.

        $ git rm --cached -r .

3. Rewrite the Git index to pick up all the new line endings.

        $ git reset --hard

4. Add all your changed files back, and prepare them for a commit. This is your chance to inspect which files, if any, were unchanged.

        $ git add .
        # It is perfectly safe to see a lot of messages here that read
        # "warning: CRLF will be replaced by LF in <file>."

5. Commit the changes to your repository.

        $ git commit -m "Normalize all the line endings"

### Git Aliases

    $ git config --global alias.co checkout
    $ git config --global alias.br branch
    $ git config --global alias.ci commit
    $ git config --global alias.st status

    $ git config --global alias.unstage "reset HEAD --"

Show history of all branch with graph

    $ git config --global alias.hist "log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short"

This makes the following two commands equivalent:

    $ git unstage fileA
    $ git reset HEAD fileA

See the last commit

    $ git config --global alias.last 'log -1 HEAD'

Template

```bash
[alias]
    # one-line log
    l = log --pretty=format:"%C(yellow)%h\\ %ad%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --date=short

    a = add
    ap = add -p
    c = commit --verbose
    ca = commit -a --verbose
    cm = commit -m
    cam = commit -a -m
    m = commit --amend --verbose

    d = diff
    ds = diff --stat
    dc = diff --cached

    s = status -s
    co = checkout
    cob = checkout -b
    # list branches sorted by last modified
    b = "!git for-each-ref --sort='-authordate' --format='%(authordate)%09%(objectname:short)%09%(refname)' refs/heads | sed -e 's-refs/heads/--'"

    # list aliases
    la = "!git config -l | grep alias | cut -c 7-"
```

```bash
[alias]
    co = checkout
    ec = config --global -e
    up = !git pull --rebase --prune $@ && git submodule update --init --recursive
    cob = checkout -b
    cm = !git add -A && git commit -m
    save = !git add -A && git commit -m 'SAVEPOINT'
    wip = !git add -u && git commit -m "WIP"
    undo = reset HEAD~1 --mixed
    amend = commit -a --amend
    wipe = !git add -A && git commit -qm 'WIPE SAVEPOINT' && git reset HEAD~1 --hard
    bclean = "!f() { git branch --merged ${1-master} | grep -v " ${1-master}$" | xargs -r git branch -d; }; f"
    bdone = "!f() { git checkout ${1-master} && git up && git bclean ${1-master}; }; f"
```

## Git Attributes

## Git Hooks

- https://git-scm.com/docs/githooks
- Centralized hooks in your local
    + https://stackoverflow.com/a/37293198/1683888
    + Set `core.hooksPath`

# Git Book

- [Git tutorials](https://www.atlassian.com/git/tutorial)

`$ git help <command>`

## Ignoring files

- Check why a file is ignored:
    + `git check-ignore -v path/to/ignored/file`
    + It will display the rule and line number that ignore this file

- [Joe command line tool](https://karan.github.io/joe/)
- [Creating ignore files online](https://www.gitignore.io/)
- [.gitignore templates](https://github.com/github/gitignore)
- Global ignore: https://gist.github.com/subfuzion/db7f57fff2fb6998a16c

A gitignore file specifies untracked files that Git should ignore. The
purpose of gitignore files is to ensure that certain files not tracked
by Git remain untracked. To stop tracking a file that is currently
tracked, use `git rm --cached <file>`.

Each line in a gitignore file specifies a **pattern**. When deciding
whether to ignore a path, Git checks gitignore patterns from multiple
sources, with the following order of precedence, from highest to lowest
(within one level of precedence, the last matching pattern decides the
outcome):
- Patterns read from the command line for those commands that support
  them.
- Patterns read from a `.gitignore` file in the same directory as the
  path, or in any parent directory, with patterns in the higher level
  files (up to the top level of the work tree) being overridden by those
  in lower level files down to the directory containing the file. These
  patterns match relative to the location of the `.gitignore` file. A
  project normally includes such `.gitignore` files in its repository,
  containing patterns for files generated as part of the project build.
    + This file should only exclude files and directories that are a
      part of the package that should not be versioned (such as the
      `node_modules` directory) as well as files that are generated (and
      regenerated) as artifacts of a build process.
- Patterns read from `$GIT_DIR/info/exclude`.
- Patterns read from the file specified by the configuration variable
  `core.excludesFile`.
    + With this we can set up the global gitignore for our machines. Any
      files created by editors, IDEs, operating systems, etc. are put in
      this file.

### Repository level: .gitignore files

Patterns which should be version-controlled and distributed to other
repositories via clone (i.e., files that all developers will want to
ignore). **Communal ignoring of repository**.

### Repository level: $GIT_DIR/info/exclude file

Patterns which are specific to a particular repository but which do not
**need/want** to be shared with other related repositories (e.g.,
auxiliary files that live inside the repository but are specific to one
user's workflow). **Personal ignoring of repository**.

### User level (Global gitignore / gitignore_global)

- In `~/.gitconfig` file
    + `core.excludesFile = <path-to-the-ignore-file>`

**core.excludesFile** default value is `$XDG_CONFIG_HOME/git/ignore`. If
`$XDG_CONFIG_HOME` is either not set or empty,
`$HOME/.config/git/ignore` is used instead.

You can create a new file and add to `~/.gitconfig` if you like:
`core.excludesFile = <path-to-the-ignore-file>`

```
#compiled source #
###################
*.com
*.class
*.dll
*.exe
*.o
*.so

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Logs and databases #
######################
*.log
*.sql
*.sqlite

# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
```

### Pattern Format

- Ignore all directory and it's files with name: `directory_name`
- Ignore only directory at root level: `/directory_name`

## Basics

### Common steps

    cd to dir
    git init
    git status
    git add <file name|*.*>
    git commit -m "message"
    git log
    git remote add origin https://..
    `git push -u origin master` : -u to remember parameter -> second time only need git push
    `git pull origin master` : update change on master branch

`git rm <files>` : remove files

switch to master branch and git merge <branch_name> to merge master with
<branch_name>

Delete remote branch:
- `git push origin --delete <branch_name>`
- `git push origin :<branch_name>`

### Tagging

- [Tag mean](http://alblue.bandlem.com/2011/04/git-tip-of-week-tags.html)

Tags in git are lightweight references that point to an SHA hash of a
commit. Unlike branches, they are not mutable and once created should
not be deleted. Tags may be lightweight (in which case they refer to the
commit directly) or annotated (in which case they point to a tag object
which points to the commit). Tags used to denote versioned releases
typically use annotated tags, and for many open source projects, the
tags will also be signed.

#### Listing your tags

`git tag`: list all tags
`git show <tag>`: show information of tag

Search for tags with a particular pattern.
`git tag -l 'v.1.8.*'`

#### Creating tags

Git uses two main types of tags: **lightweight** and **annotated**.

- A lightweight tag is very much like a branch that doesn't change - it's just a pointer to a specific commit.
`git tag v1.4-lw`

- Annotated tags, however, are stored as full objects in the Git database. They're cheksummed; contain the tagger name, e-mail, and data; have a tagging message; and can be sined and verified with GPG.
`git tag -a v1.4 -m 'my version 1.4'`

Tag a commit in history: `git tag -a v1.2 9fceb01`

#### Sharing tags

`git push origin [tagname]`
`git push origin --tags`

#### Checking out tags

`git checkout -b version2 v2.0.0`

#### Delete tags

`git tag -d <tagname>`


### Undoing things

#### Common undoing

`git reset`: will rewrite your history

`git revert` : add new commits record revert process, do not change your history

`git reset --hard <commit>` : will move your HEAD pointer, reset your change, index

`git reset <commit>` : will move your HEAD pointer, keep your change, reset your index

`git reset --soft <commit>` : will move your HEAD pointer, keep your change and index

#### Reverting multiple commits

- Commit history: `a -> b -> c -> d (HEAD)`
    + Want to revert to `a`

```
# This will work  for every types of commit
git reset --hard a
git reset --soft d
git commit

# Using git revert, will not work for merge commits
git revert --no-commit HEAD~4..
git commit
```

- This trick relies on Git to find the differences between a hard reset
  and a soft reset, and we can treats those changes as revert changes.
- In the essence, the hard reset discards changes in index and working
  tree and reverts commits in the local repository. While the soft reset
  only moves the HEAD reference and does not touch the commit
  history. Therefore, when we do a soft reset after a hard reset, then
  the changes in the index is the revert changes the hard reset
  performed to revert commit history, so from there we can reuse it as a
  new commit to revert our changes.
- This trick always works.
- `git revert <commit>` only works with non-merge commits, if there are
  merge commits, you cannot revert multiple commits using `git revert`.
    + Read `man git-revert` to know more how to revert a merge commit
      using `git revert`

#### Reverting working copy to most recent commit

`git reset --hard HEAD`

#### Undo add all file

`git reset`

#### Undo a commit and redo

    git commit ...
    git reset --soft HEAD^
    edit sth
    git commit -ac ORIG_HEAD

#### Commit too early forget to add some files

`git commit --amend`

This command takes your staging area and uses it for the commit. If
you've made no changes since your last commit (for instance, you run
this command immediately after your previous commit), then your snapshot
will look exactly the same, and all you'll change is your commit
message.

As an example, if you commit and then realize you forgot to stage the
changes in a file you wanted to add to this commit, you can do something
like this:

    $ git commit -m 'initial commit'
    $ git add forgotten_file
    $ git commit --amend

#### Unstaging a staged file - undo add a file

`git reset -- <file name>` : unstaged file (opposite with git add)

#### Unmodifying a modified file

`git checkout -- <file name>`

#### Unpushing a pushed commit

`git push <remote> +<sha1>^:<branch name>`

`git push origin +ba8342^:feature/emp_detail`

where `x^` as the parent of `x` and `+` as a forced non-fast-forward
push.

**Another way**: Rewrite history at local and force push to replace a
new commit
1. Rewrite history: for example `git reset --hard HEAD~1` : undo the
   last commit
2. Force push: `git push -f <remote> <branch>`

#### Temporarily switch to a different commit

If you want to temporarily go back to it, fool around, then come back to
where you are, all you have to do is check out the desired commit:

    # This will detach your HEAD, that is, leave you with no branch
      checked out: git checkout 0d1d7fc32

Or if you want to make commits while you're there, go ahead and make a
new branch while you're at it:

    git checkout -b old-state 0d1d7fc32

#### Hard delete unpublished commits

If, on the other hand, you want to really get rid of everything you've
done since then, there are two possibilities. One, if you haven't
published any of these commits, simply reset:

    # This will destroy any local modifications.
    # Don't do it if you have uncommitted work you want to keep.
    git reset --hard 0d1d7fc32

    # Alternatively, if there's work to keep:
    git stash
    git reset --hard 0d1d7fc32
    git stash pop
    # This saves the modifications, then reapplies that patch after resetting.
    # You could get merge conflicts, if you've modified things which were
    # changed since the commit you reset to.

#### Undo published commits with new commits

On the other hand, if you've published the work, you probably don't want
to reset the branch, since that's effectively rewriting history. In that
case, you could indeed revert the commits. With Git, revert has a very
specific meaning: create a commit with the reverse patch to cancel it
out. This way you don't rewrite any history.

    # This will create three separate revert commits:
    git revert a867b4af 25eee4ca 0766c053

    # It also takes ranges. This will revert the last two commits:
    git revert HEAD~2..HEAD

    # Reverting a merge commit
    git revert -m 1 <merge_commit_sha>

    # To get just one, you could use `rebase -i` to squash them afterwards
    # Or, you could do it manually (be sure to do this at top level of the repo)
    # get your index and work tree into the desired state, without changing HEAD:
    git checkout 0d1d7fc32 .

    # Then commit. Be sure and write a good message describing what you just did
    git commit

## Branching

- [Git Branching](https://git-scm.herokuapp.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)

`git branch -a` : list all branch

`git branch -r` : list all remote branch

`git branch -d <branch_name>` : delete a branch after merge

`git branch -D <branch_name>` : force delete a branch not yet merge

`git branch <branch_name>` : create new branch

`git checkout <branch_name>` : switch to another branch

**git checkout -b <branch_name>** : create new branch and checkout to it


## Git on the Server

### The Protocols

#### Local protocol


#### The HTTP Protocol

##### Smart HTTP (HTTPS)

use username/password to authentication

##### Dump HTTP

If the server does not respond with a Git HTTP smart service, the Git
client will try to fall back to the simpler “dumb” HTTP protocol. The
Dumb protocol expects the bare Git repository to be served like normal
files from the web server. The beauty of the Dumb HTTP protocol is the
simplicity of setting it up. Basically, all you have to do is put a bare
Git repository under your HTTP document root and set up a specific post-
update hook, and you’re done (See “Git Hooks”). At that point, anyone
who can access the web server under which you put the repository can
also clone your repository. To allow read access to your repository over
HTTP, do something like this:

    $ cd /var/www/htdocs/
    $ git clone --bare /path/to/git_project gitproject.git
    $ cd gitproject.git
    $ mv hooks/post-update.sample hooks/post-update
    $ chmod a+x hooks/post-update

That’s all. The post-update hook that comes with Git by default runs the
appropriate command (git update-server-info) to make HTTP fetching and
cloning work properly. This command is run when you push to this
repository (over SSH perhaps); then, other people can clone via
something like

`$ git clone https://example.com/gitproject.git`

#### The SSH Protocol

To clone a Git repository over SSH, you can specify ssh:// URL like this:

    $ git clone ssh://user@server/project.git

#### The Git Protocol

lack of authentication, only use to clone repository because fastest
network transfer protocol.


### Set up a Git server

#### Simple Git server without GUI

1. Add use git in Git server:
    `useradd git`
    `passwd git`
2. Install git in Git server:
    - CentOS/Fedora: `yum install git`
    - Ubuntu/Debian: `apt-get install git`
3. Add SSH key of local machine want access to Git server
    - `mkdir ~/.ssh && touch ~/.ssh/authorized_keys`
4. Set up a repository
    `git init --bare my-project.git`
5. Using Git server
    `git remote set-url origin git@192.168.88.223:/my-project/my_project.git`


### Setup SSH for Git

- Step 1: Check if you have existing default Identity
    + `ls -la ~/.ssh`
    + if you see id_rsa, id_rsa.pub known_hosts then the default
      identity use RSA encryption.
- Step 2: Set up an identity
    + `$ ssh-keygen`
- Step 3: Edit your `.bashrc` file
    + This file start ssh-agent and add your key help you don't need
      type your passphrase each time you push commit to remote.
    + Contents of .bashrc

```bash
# The location to store the output of `ssh-agent`
SSH_ENV=$HOME/.ssh/environment

# start the ssh-agent
function start_agent {
    echo "Initializing new SSH agent..."
    # spawn ssh-agent
    /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
    echo succeeded
    chmod 600 "${SSH_ENV}"
    . "${SSH_ENV}" > /dev/null
    /usr/bin/ssh-add
}

# if there is a running ssh-agent, then execute the output of
# `ssh-agent` to export the SSH environment variables (SSH_AUTH_SOCK,
# SSH_AGENT_PID)
# else start a new ssh-agent
if [ -f "${SSH_ENV}" ]; then
    . "${SSH_ENV}" > /dev/null
    # confirm that the ssh-agent is still running, if not, then start a
    # new agent.
    ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
        start_agent;
    }
else
    start_agent;
fi
```

- Step 4: Install public key to your remote

### GitWeb

### GitLab

### [Third party hosting](https://git.wiki.kernel.org/index.php/GitHosting)


# Workflows, Contributing and Maintaining a Project

- [Git workflows](https://www.atlassian.com/git/workflows)

## Centralized Workflow

Exact same as Subversion. Appropriate with few developers.

- The default development branch is called `master`.
- Developers start by cloning the central repository. In their local
  copies of the project, they edit files and commit changes as they
  would with SVN; however, these new commits are stored locally -
  they're completely isolated from the central repository. This lets
  developers defer synchronizing upstream until they're at a convenient
  break point.
- Before publish changes, developers must update central commits and
  rebase their changes on top of them. `git pull --rebase origin
  master`. If have conflict, developers must solve it to continue.
- To publish changes to the official project, developers    `push` their
  local master branch to the central repository. `git push origin
  master`

![Centralized workflow](https://github.com/samtron1412/figures/raw/master/git/centralized.png "Centralized workflow")

## Integration-Manager Workflow

1. The project maintainer pushes to their public repository.
2. A contributor clones that repository and makes changes.
3. The contributor pushes to their own public copy. (forked)
4. The contributor sends teh maintainer a pull request.
5. The maintainer adds the contributor's repo as a remote and meres
   locallly.
6. The maintainer pushes merged changes to the main repository.

![Integration-manager workflow](https://github.com/samtron1412/figures/master/git/integration-manager.png "Integration-manager workflow")

This is very common workflow with hub-based tools like GitHub or GitLab.

## Dictator and Lieutenants Workflow

It's generally used by huge projects with hundreds of collaborators; one
famous example is the Linux kernel.

1. Regular developers work on their topic branch and rebase their work
   on top of `master`. The `master` branch is that of the dictator.
2. Lieutenants merge the developers' topic branches into their `master`
   branch.
3. The dictator merges the lieutemants' `master` branches into the
   dictator's `master` branch.
4. The dictator pushes their `master` to the references repository so
   the other developers can rebase on it.

![Benevolent dictator workflow](https://github.com/samtron1412/figures/raw/master/git/benevolent-dictator.png "Benevolent dictator workflow")


## Feature branch Workflow

Appropriate with more developers. Each branch correspond with each
features beside `master` branch. This leverage pull requests, which are
a way to discussions around a branch.

- Developers create a new branch every time they start work on a new
  feature. Feature branches should have descriptive names, like
  `animated-menu-items` or `issue-#1061`. Highly focused purpose to each
  branch.
- Each branch, developers can do anything like the Centralized Workflow.
- Feature branches can be pushed to the central repository. This makes
  it possible to share a feature with other developers without touching
  any official code.
- Aside from isolating feature, branches make it possible to discuss
  changes via `pull requests`. Once someone completes a feature, they
  don't immediately merge it into `master`. Instead, they push the
  feature branch to the central server and file a pull request asking to
  merge their additions into `master`. This gives other developers an
  opportunity to review the changes before they become apart of the main
  codebase.
- Once pull request is accepted, the actual act of publishing a feature
  is much the same as in the Centralized Workflow. First, local master
  us synchronized with the upstream master. Then, merge the feature
  branch into master and push the updated master back to the central
  repository.

## Gitflow Workflow

A strict branching model designed around the project release. More
complicated than the Feature Branch Workflow, this provides a robust
framework for managing larger projects.

![Gitflow](https://github.com/samtron1412/figures/raw/master/git/git-model@2x.png)

- This work flow assigns very specific roles to different branches and
  defines how and when they should interact. In addition to feature
  branches, it uses individual branches for preparing, maintaining, and
  recording releases.
- **Main branches**, Uses two branches to record the history of the
  project. The `master` branch stores the official release history, and
  the `develop` branch serves as an integration branch for features.
  It's also convenient to tag all commits in the `master` branch with a
  version number. ![History project](https://github.com/samtron1412/figures/raw/master/git/02.svg)
- **Feature Branches**, new feature will have its own branch. But,
  instead of branching off of `master`, feature branches use `develop`
  as their parent branch. When feature is complete, it gets merged back
  into `develop` branch. Features should never interact directly with
  `master`. Delete feature branches after merged to `develop` branch.
  ![Feature branches](https://github.com/samtron1412/figures/raw/master/git/03.svg)
- **Release branches**, once `develop` has acquired enough features for
  a release ( or a predetermined release date is approaching), you fork
  a release branch off of `develop`. Creating this branch starts the
  next release cycle, no new features can be added after this point -
  only **bug fixes**, **documentation**, and other **release-oriented
  tasks** should go in this branch. Once it's ready to ship, the release
  gets merged into `master` and tagged with a version number. In
  addition, it should be merged back into `develop`, which may have
  progressed since the release was initiated.
    + This term makes it possible for one team to polish the current
      release while another team continues working on features for the
      next release.
    + naming: `release-*` or `release/*`
    + Tagged a version number after merged back into `master` and
      `develop` branch: `git push --tags`
    + Delete release branch after release.

![Release branch](https://github.com/samtron1412/figures/raw/master/git/04.svg)

- **Maintenance branches** (hotfix branches), used to quickly patch
  production releases. This is the only branch that should fork directly
  off of `master`. As soon as the fix is completer, it should be merged
  into both `master` and `develop` (or the current release branch), and
  `master` should be tagged with an updated version number. Naming:
  `issue-#001`

![Hotfix branch](https://github.com/samtron1412/figures/raw/master/git/05.svg)

## Forking Workflow

Every developer have a server-side repository. Each contributor has two
Git repositories: a private local one and a public server-side one.

- Benefit is: the contributions can be integrated without the need for
  everybody to push to a single central repository. Developers push to
  their own server-side repositories, and only the project maintainer
  can push to the official repository. This allows the maintainer to
  accept commits from any developer without giving them write access to
  the official codebase.
- Privides a flexible way for large, organic teams (including untrusted
  third-parties) to collaborate securely. ideal work flow for open
  source projects.

## Pull request

Pull requests are a feature that makes easier for developers to
**collaborate**. They provide a user-friendly interface for
**discussing** proposed changes before integrating them into the
official project. In their simplest form, pull requests are a mechanism
for a developer to **notify** team members that they have completed a
feature.

But, the pull request is more than just a notification — it's a
dedicated forum for discussing the proposed feature. If there are any
problems with the changes, teammates can post feedback in the pull
request and even tweak the feature by pushing **follow-up commits**. All
of this activity is tracked directly inside of the pull request.

### How It Works

Pull requests can be used in conjunction with the **Feature Branch
Workflow**, the **Gitflow Workflow**, or the **Forking Workflow**. But a
pull request requires either *two distinct branches or two distinct
repositories*, so they will not work with the **Centralized Workflow**.
Using pull requests with each of these workflows is slightly different,
but the general process is as follows:

1. A developer creates the feature in a dedicated branch in their local
   repo.
2. The developer pushes the branch to a public repository.
3. The developer fire a pull request.
4. The rest of the team reviews the code, discusses it, and alters it.
5. The project maintainer merges the feature into the official
   repository and closes the pull request.

The rest of this section describes how pull requests can be leveraged
against different collaboration workflows.

## Contributing to a Project

### Commit

- Use `git diff --check` to check whitespace errors.
- Try to make each commit a logically separate changeset. Make your
  changes digestible.
    + Use staging area to split your work.
    + `git add --patch`
- [Git commit message structure](https://web.archive.org/web/20150330043110/http://chris.beams.io/posts/git-commit/)
- Tools
    + commitlint:
        * https://commitlint.js.org
        * https://www.conventionalcommits.org
        * https://www.freecodecamp.org/news/how-to-use-commitlint-to-write-good-commit-messages/
    + commitizen
        * https://github.com/commitizen/cz-cli
        * https://dev.to/sohandutta/make-everyone-in-your-project-write-beautiful-commit-messages-using-commitlint-and-commitizen-1amn
- Automate commit message
    + Setting `commit.template` in `~/.gitconfig`
    + Create `~/.gitmessage` with folowing content

```
# ~/.gitconfig
[commit]
  template = ~/.gitmessage

# ~/.gitmessage

Capitalized imperative summary (<= 50 characters, no period at the end)

More detailed explanatory text, if necessary (What?)
 - Wrap it to about 72 characters

Why do you make this change?
 - The problem of current code
 - The solution

Are there any side effects or unintuitive consequences?

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789

```


```
# 50-character subject line
#
# 72-character wrapped longer description. This should answer:
#
# * Why was this change necessary?
# * How does it address the problem?
# * Are there any side effects?
#
# Include a link to the ticket, if any.
#
# Add co-authors if you worked on this code with others:
#
# Co-authored-by: Full Name <email@example.com>
# Co-authored-by: Full Name <email@example.com>
```

```
Summarize changes in around 50 characters or less (no period at the end)
 - e.g.: Fix dropdown menu of the main webpage
 - e.g.: Revert the changes on the submit form
 - e.g.: Update the changes on the submit form

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

#### Conventional commits message types

- https://www.conventionalcommits.org

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

```
feat: {
        description: 'A new feature',
},
fix: {
        description: 'A bug fix',
},
docs: {
        description: 'Documentation only changes',
},
style: {
        description:
                'Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)',
},
refactor: {
        description:
                'A code change that neither fixes a bug nor adds a feature',
},
perf: {
        description: 'A code change that improves performance',
},
test: {
        description: 'Adding missing tests or correcting existing tests',
},
build: {
        description:
                'Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)',
},
ci: {
        description:
                'Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)',
},
chore: {
        description: "Other changes that don't modify src or test files",
},
revert: {
        description: 'Reverts a previous commit',
},
```

### Private small team

![Small Team Workflow Simple](https://github.com/samtron1412/figures/raw/master/git/small-team-flow.png "Small Team Workflow Simple")

### Private managed team

![Small Team Workflow Complex](https://github.com/samtron1412/figures/raw/master/git/managed-team-flow.png "Small Team Workflow Complex")

## Maintaining a Project

- Accepting and applying patches generated via `format-patch` and
  e-mailed to you
- Integrating changes in remote branches for repositories you've added
  as remotes to your project.

Patch Workflow
![Patch Workflow](https://github.com/samtron1412/figures/raw/master/git/patch-workflow.png)

### Working in Topic Branches


### Applying Patches from E-mail

#### Applying a Patch with `git apply`

#### Applying a Patch with `git am`


### Checking out remote branches

### Determining What is introduced

### Integrating Contributed work

#### Merging Workflows

#### Large-Merging Workflows

#### Rebasing and Cherry Picking Workflows

#### Rerere - reuse recorded resolution

### Tagging Your Releases

### Generating a Build Number

### Preparing a Release

# Git Tools

## Credential Storage

Credential helpers:
- `cache`: store credential in memory and delete after xxx second.
  (Inconvenient when using with 2FA)
    + `$ git config --global credential.helper cache`
    + Default is 900s, we can add time:
        * `git config --global credential.helper "cache --timeout 36000"`
- `store`: saves the credentials to a **plain-text** file on disk, and
  they never expire. Passwords are stored in cleartext in a plain file.
  (Supper dangerous method, no security)
- `osxkeychain`: Mac OS
- `wincred`: work on Windows. Use it for Windows system.
- `git-credential-gnome-keyring`: need to compile it
    + `$ cd /usr/share/git/credential/gnome-keyring`
    + `# make`
    + `$ git config --global credential.helper /usr/lib/git-core/git-credential-gnome-keyring`
- `git-credential-netrc`

### Under the Hood


### A Custom Credential Cache

You can write your own credential helper.

# Hosting Services

## Why?

- Workspace for collaborators: pull requestsm, news feed,...
- Wiki
- Bug tracking

## Hosting services

- GitHub
- Bitbucket
- Google code
- Command line for different hosts
    + https://i.got.nothing.to/code/on/git-repo:_the_utility_for_services/

## Private Git server

### Installation and Configuration server Git


### [Open source GitHub-like interface](https://git.wiki.kernel.org/index.php/Interfaces,_frontends,_and_tools#Web_Interfaces)

- [gogs](https://github.com/gogits/gogs)
- [GitLab](https://about.gitlab.com/)
- [GitBucket](https://github.com/gitbucket/gitbucket)
    + http://www.slideshare.net/takezoe/scala-matsuri-gitbucket
- [cgit](http://git.zx2c4.com/cgit/) (use for Linux kernel)
- [gitlist](https://github.com/klaussilveira/gitlist)
- [gitolite](https://github.com/sitaramc/gitolite)


# Git and Other Systems

## Migration to Git

### SVN to Git

#### [Atlassian](https://www.atlassian.com/git/migration)

[Detail script code](http://blogs.atlassian.com/2012/01/moving-confluence-from-subversion-to-git/)

We’ve broken down the SVN-to-Git migration process into 5 simple steps:

1. Prepare your environment for the migration.
2. Convert the SVN repository to a local Git repository.
3. Synchronize the local Git repository when the SVN repository changes.
4. Share the Git repository with your developers via Bitbucket.
5. Migrate your development efforts from SVN to Git.

With small developer team and the frequency of commit is low we can skip
step 3 and 4.

##### Prepare

- Download script use to migrate [here](https://bitbucket.org/atlassian/svn-migration-scripts/downloads)
- Verify environment: `java -jar svn-migration-scripts.jar verify`
- Extract authors information:
    + `java -jar ~/svn-migration-scripts.jar authors <svn-repo> > authors.txt`
    + `java -jar ~/svn-migration-scripts.jar authors https://svn.example.com > authors.txt`
    + `java -jar ~/svn-migration-scripts.jar authors https://redmine.ig.webike.net/svn/repos > authors.txt`
- Edit authors.txt file:

        j.doe = j.doe <j.doe@mycompany.com>
        m.smith = m.smith <m.smith@mycompany.com>

        j.doe = John Doe <john.doe@atlassian.com>
        m.smith = Mary Smith <mary.smith@atlassian.com>

##### Convert

**Import SVN to Git with git svn clone**

- With standard Subversion layouts: `/trunk`, `/branches`, and `/tags` directory layout
    + `git svn clone --stdlayout --authors-file=authors.txt <svn-repo>/<project> <git-repo-name>`
    + `git svn clone --stdlayout --authors-file=authors_community.txt https://redmine.ig.webike.net/svn/repos/community community`
- With non-standard Subversion layouts:
    + `git svn clone --trunk=/trunk --branches=/branches --branches=/bugfixes --tags=/tags --authors-file=authors.txt <svn-repo>/<project> <git-repo-name>`
    + `git svn clone --trunk=/trunk/Community --trunk=/trunk/CommunityAdmin --trunk=/trunk/community_conf --branches=/branches/Community(ImpressionRenewal_JP) --branches=/branches/Community.PHP_Dev --branches=/branches/Community_Dev --tags=/tags/... --authors-file=authors_community.txt https://redmine.ig.webike.net/svn/repos community`
- Use `git branch -r` to show all branch of new git repository.
    + Branches and tags are not imported into the new Git repository
    + The `git svn clone` command imports your SVN branches as remote
      branches and imports your SVN tags as remote branches prefixed
      with `tags/`.

##### Clean the new Git repository

The `clean-git` script included in `svn-migration-scrits.jar` turns the
SVN branches into local Git branches and the SVN tags into full-fledged
Git tags.

- See what can be cleaned up:

`java -Dfile.encoding=utf-8 -jar ~/svn-migration-scripts.jar clean-git`

- To execute these changes, you need to use the `--force` option:

`java -Dfile.encoding=utf-8 -jar ~/svn-migration-scripts.jar clean-git --force`


##### Troubleshoot

###### svn: E200009: "Could not list all targets because some targets don't exist"

https://answers.atlassian.com/questions/248517/cloning-svn-to-bitbucket-branches-are-not-created-in-git

#### [Svn2Git](https://techbase.kde.org/Projects/MoveToGit/UsingSvn2Git)


#### [Subgit](http://www.subgit.com/)

# Git Internals


# Cheatsheet

## git-stash - stash changes in working directory away

- `git stash push -m "message" -- filename.ext`: stash a file
- `git stash`: stash all changes
- `git stash show`: show the files in the most recent stash
- `git stash show -p`: show the changes of the most recent stash
- `git stash show -p stash@{1}`: show the changes of the named stash
    + `git stash show -p 1`

## git-diff - show changes between commits, commit and working tree, etc.

### Check your working tree

- `git diff`: Show differences between your working directory and the
  index.
- `git diff <old commit> <new commit>`: show changes / differences that
  the new commit makes on top of the old commit.
- `git diff --cached`: Show differences between the index and the most
  recent commit.
- `git diff HEAD`: Show the differences between your working directory
  and the most recent commit.
- `git difftool`: See a visual representation of the differences by
  using tools such as `vimdiff`.

### Comparing with arbitrary commits

- https://git-scm.com/docs/git-rev-parse#_specifying_revisions
    + Specifying a revision.
- `~` is used to go number of generation back
    + `~` or `~1`: go back 1 generation
    + `~2`: go back 2 generations
- `^` is used on merge commits where a commit can have more than 1
  parent. Hence, looks like forks in a road.
    + `^` or `^1`: first parent
    + `^2`: second parent
    + `^3`: third parent
- https://git-scm.com/docs/git-rev-parse#_revision_range_summary
    + Range of revisions.

- `git diff HEAD^ HEAD`: Compare the `HEAD` commit and `HEAD's` first
  parent.
- `git diff HEAD^2 HEAD`: Compare the `HEAD` commit and `HEAD's` second
  parent.
- `git diff HEAD^^ HEAD`: Compare the `HEAD` commit and `HEAD's` first
  grandparent.
    + `HEAD^` is a short hand for `HEAD^1`
- `git diff HEAD^^^ HEAD`: Compare the `HEAD` commit and `HEAD's` first
  great grandparent.
- `git diff HEAD^^^2 HEAD`: Compare the `HEAD` commit and `HEAD's`
  second great grandparent.
- `git diff HEAD^^^3 HEAD`: Compare the `HEAD` commit and `HEAD's`
  second third grandparent.


- `git diff HEAD~3 HEAD`: Show the last three commits changes.

- `git diff HEAD -- test.md`: Show the differences between your working
  directory and the most recent commit, but limit the comparison to the
  file `test.md`.

### Comparing branches

- `git diff branch1 master` or `git diff branch1..master`: Show
  differences between two branches.
- `git diff branch1...master`: Show changes that occurred on the master
  branch since when the branch1 branch was started off it.

### Limiting the diff output

- `git diff --diff-filter=MRC`: Show only modification, rename, and
  copy, but not addition or deletion. Possible status letters: `man git-
  diff` and search for **status letters**.

### Misc

- `git diff -R`: Show diff output in reverse

## git-apply - Apply a patch to files and/or to the index

- When running from a subdirectory in a repository, patched paths
  outside the directory are ignored.
- With the `--index` option the patch is also applied to the index, and
  with the `--cached` option the patch is only applied to the index.
  Without these options, the command applies the patch only to files,
  and does not require them to be in a git repository.
- This command applies the patch but does not create a commit. Use `git-
  am` to create commits from patches generated by `git-format-patch`
  and/or received by email.

- `git apply --stat xdg-utils-v1.1.1.patch`: Show diffstat instead of
  applying the patch
- `git apply --check xdg-utils-v1.1.1.patch`: Check if the patch is
  applicable toe the current working tree and/or the index and detects
  errors.
- `git apply xdg-utils-v1.1.1.patch`: Apply the patch
- `git apply -R some.path`: revert the patch

## git-format-patch - Prepare patches for e-mail submission

- Preparing each commit with its patch in one file per commit, formatted
  to resemble UNIX mailbox format.
- The output of this command is convenient for e-mail submission or for
  use with `git am`.
- `git format-patch -3`: Extract three topmost commits from the current
  branch and format them as e-mailable patches.
- `git format-patch -3 --stdout > new.patch`: Only create one patch from
  3 commits.
- `git format-patch -s -1`: Extract the latest commit from the current
  branch and add line **Signed-off-by: John Doe <john@doe.com>** to the
  end of the commit log message.

## git-am - Apply the series of patches from a mailbox

- Splits mail messages in a mailbox into commit log message, authorship
  information and patches, and applies them to the current branch.
- `git am < new.patch`: Apply a patch to the current branch.
- `git am --abort`: Restore the original branch and abort the patching
  operation.
- `git am <Maildir>`: Apply all patches in the Maildir.
- `git am *.patch`: Apply all patch.


## git-archive - Create an archive of files from a named tree

Creating an archive of the specified format containing the tree
structure for the named tree, and writes it out to the standard output.
- `git archive --format=tar --prefix=junk/ HEAD | (cd /var/tmp/ && tar xf -)`: Creating a tar archive that contains the contents of the latest commit on the current branch, and extract it in the `/var/tmp/junk` directory.
- `git archive --format=tar --prefix=git-1.4.0/ v1.4.0 | gzip >git-1.4.0.tar.gz`: Creating a compressed tarball for v1.4.0 release.
- `git archive --format=tar.gz --prefix=git-1.4.0/ v1.4.0 >git-1.4.0.tar.gz`: Creating a compressed tar.gz for v1.4.0 release.
- `git archive --prefix=git-1.4.0/ -o git-1.4.0.tar.gz v1.4.0`: Same as above, but the format is inferred from the output file.
- `git archive --format=tar.gz --prefix=git-docs/ v1.4.0:Documentation/ > git-1.4.0-docs.tar.gz`: Put everything in the current head's Documentation/ directory into git-1.4.0-docs.tar.gz, with the prefix `git-docs/`.
- `git archive -o latest.tar.gz HEAD`: Creating a tarball that contains the contents of the latest commit on the current branch.

## git-send-email - Send a collection of patches as emails

Takes the patches given on the command line and emails them out. Patches
can be specified as files, directories (which will send all files in the
directory), or directly as a revision list.

`~/.gitconfig`
```
[sendemail]
    smtpEncryption = tls
    smtpServer = smtp.gmail.com
    smtpUser = yourname@gmail.com
    smtpServerPort = 587
    suppresscc = self
    confirm = always
```

If you have multifactor authentication setup on your Gmail account, you
will need to generate an app-specific password for use with git-send-
email. Visit
[here](https://security.google.com/settings/security/apppasswords) to
setup an app-specific password.

- `git send-email -1`: Sending the last commit in the current branch.
- `git send-email -1 <commit reference>`: Sending some other commit.
- `git send-email -10 --cover-letter --annotate`: Sending the last 10
  commits in the current branch.
    + `--cover-letter` creates an extra mail that will be sent before
      the actual patch mails. You can add some introduction to the patch
      set in the cover letter. It's fine to only have the shortlog that
      is included in the cover letter by default, and only set the
      `Subject` header to something sensible.
    + `--annotate` causes an editor to be started for each of the mails,
      allowing you to edit the mails. The option is always necessary, so
      that you can edit the cover letter's `Subject` header.
- `git send-email --to <email-address> outgoing/*`: Send all patches in
  outgoing directory.

# git-filter-repo: History rewriting tools and libraries

- https://github.com/newren/git-filter-repo
- Install
    + macOS or Linux (using Home brew)
        * `brew install git-filter-repo`

## Applications

- https://github.com/newren/git-filter-repo/tree/main/contrib/filter-repo-demos
- Split files/directories to a new repository.
    * git-subtree: https://stackoverflow.com/a/17864475
- Remove files/directories from history.
- Modify / Update history

## Filter Git histories for certain files and directories

- https://stackoverflow.com/a/59832729
    + There is a `git-filter.sh` script in `pri-scripts` repository to
      use.
- This can be done first, and then combine with the next section, we can
  move these files and histories to a new repository.
    + So first, filter Git history for files and directories.
    + Then move these files and directories to new repository.

## Move files/directories to another existing repository.

- https://stackoverflow.com/a/61917589
- After the previous step of `Filter Git histories` above, we can merge
  or rebase that filtered history to the new repository.
- There are 3 or 2 time records associated with each commit:
    + Author time: when the change was originally authored/created.
        * Remains unchanged even if the commit is amended or rebased.
    + Commit time: when the commit was last modified
        * Changes when you amend a commit or rebase
        * Represents when the commit was actually added to the
          repository.
    + Push time (non-native to Git, supported in some Git platforms such
      as GitHub/GitLab): time when the commit is pushed to the remote.
- Merge will not change both author time and commit time, but rebase
  will change commit time.
    + So prefer Merge over Rebase whenever it's possible (sometimes, you
      can use merge because you don't want to change history)

### Merge

- In order to move `source_project/sub/dir` to `destination_project/sub/dir`:
- Steps:
    + Filter the old_repo git history using `git-filter-repo` for
      selected files and directories.
    + add the old repository/branch as a remote
    + fetch old_repo/branch
    + merge remotes/old_repo/mainline and mainline
    + push normally or send out code review and merge later

1. Create a new repo containing only the subdirectory:

```sh
git clone URL source_project
cd source_project
git filter-repo --path sub/dir

# OR using git-filter in pri-scripts/bin
git-filter -n source_project -k keep-file.txt
```

2. Merge the new repo:

```sh
git clone URL destination_project
cd ../destination_project

// create a new branch to work on it
git checkout -b filtered-destination

git remote add source-remote ../source_project
git fetch source-remote mainline
git merge remotes/source-remote/mainline --allow-unrelated-histories
git remote remove tmp
```

### Rebase

- Can introduce multiple commits with same commit messages in the
  history if many files shared one commit in the history (such as the
  first commit to create the repository)
- Steps:
    + Filter the old_repo git history using `git-filter-repo` for
      selected files and directories.
    + add the old repository/branch as a remote
    + fetch old_repo/branch
    + create a new branch track old_repo/branch
    + rebase the new branch and mainline
    + checkout mainline and merge the new branch with it
    + push normally or send out code review and merge later

```sh
```

# Git Clients

- `git` CLI
- Sublime Merge
    + https://www.sublimemerge.com/

# Tips and Tricks

## Ignoring mass reformatting commits with git blame

- https://akrabat.com/ignoring-revisions-with-git-blame/
- `git config blame.ignoreRevsFile .git-blame-ignore-revs`
- https://git-scm.com/docs/git-config#Documentation/git-config.txt-blameignoreRevsFile

```
# Run code through black
825ba00bb95c0a9bb801ccb4c6dd74ec7b59b59e

# Resolve various style issues
a6aff6bf8da21a4e6377238ae95b3c9bb941d655
```

## See the list of commit differences between branches

- https://stackoverflow.com/questions/13965391/how-do-i-see-the-commit-differences-between-branches-in-git
- `git log --online master..brranchX`

## Listing all files for a specific branch

- `git ls-tree -r <branch-name> --name-only`
- `git ls-tree -r HEAD --name-only`

## Copy commit content from another branch to your staging area

- `git cherry-pick -n <commit-hash>`
- `git reset` to clear the index

## Recover commits / changes after `git reset --hard`

- https://stackoverflow.com/questions/5788037/recover-from-losing-uncommitted-changes-by-git-reset-hard
- Using `git reflog show`
- Then `git reset HEAD@{x}`

## Ignore bulk change commits with git-blame

- https://www.moxio.com/blog/43/ignoring-bulk-change-commits-with-git-blame

## Remove untracked files

- Preview untracked files will be removed: `git clean -nd`
- Remove untracked files: `git clean -fd`

## Remove a specific commit in git history

```bash
git rebase --onto "<commit-id>^" <commit-id> HEAD
```

## Splitting a subfolder out into a new repository

- Use `filter-repo` tool instead.
- [filter-branch manual](https://git-scm.com/docs/git-filter-branch)
- [GitHub tutorial](https://help.github.com/articles/splitting-a-subfolder-out-into-a-new-repository/)
- [Moving files from one Git repository to another](http://gbayer.com/development/moving-files-from-one-git-repository-to-another-preserving-history/)

    git clone <repo>
    cd <repo>
    git remote rm origin
    git filter-branch --subdirectory-filter <folder> -- --all
    git remote add origin <url>
    git push origin master

## Change author of commit

- Change author of the last commit
    + `git commit --amend --author "Author Name <email@email.com>"`
- Other scenarios: not the last commit
    + https://stackoverflow.com/questions/3042437/how-can-i-change-the-commit-author-for-a-single-commit
    + Have to rewrite history for this to work.

## Change timestamp of commit

You may be wondering what the difference is between `author` and
`committer`. The author is the person **who originally wrote the work**,
whereas the committer is the person **who last applied the work**. So,
if you send in a patch to a project and one of the core members applies
the patch, both of you get credit – you as the author, and the core
member as the committer.

The `author date` notes when this commit was **originally made** (i.e.
when you finished the **git commit**). According to the docs of git
commit, the author date could be overridden using the `--date` switch.

The `commit date` gets changed every time the commit is **being
modified**, for example when **rebasing** the branch where the commit is
in on another branch.

Same could happen if you make your commit and send your patch to another
one in order to apply the patch in another repo: the author date will be
the date of your git commit, the commit date will be set to that date
when the patch is applied in the other repo.

`$ git commit --date="Wed Feb 16 14:00 2016 -0700"`: this only change Author Date
`$ GIT_COMMITTER_DATE="Wed Feb 16 14:00 2016 -0700" git commit --amend`: this will change committer Date
`$ GIT_COMMITTER_DATE="Sun May 1 14:00 2016 -0700" git commit --date="Sun May 1 14:00 2016 -0700"`: change both date

## Managing multiple repositories

- https://github.com/fabioz/mu-repo
- https://github.com/earwig/git-repo-updater
- https://github.com/prydonius/karn
- https://github.com/badele/gitcheck
- https://github.com/esrlabs/git-repo
- https://github.com/mixu/gr
- https://github.com/joeyh/myrepos

## Commit history of a specific file

All the history of the file after renamed:
    + `git log <filename>`

All the history of the file including the history before renamed:
    + `git log --follow <filename>`

All the history and the patches (diffs)
    + `git log --follow -p <filename>`
    + `git log -p <filename>`

Using GUI:
    + `gitk <filename>`
    + `gitk --follow <filename>`

## Remove sensitive data - Removing files from a repository's history

- [GitHub help](https://help.github.com/articles/removing-files-from-a-repository-s-history/)
- [Remove sensitive data](https://help.github.com/articles/remove-sensitive-data/)
- [BFG-repo-cleaner](https://github.com/rtyley/bfg-repo-cleaner)

## Show commit count

`git rev-list HEAD --count`

## [Commit to multiple branches at the same time](http://stackoverflow.com/questions/7259135/git-commit-to-multiple-branches-at-the-same-time)

[git cherry-pick](http://git-scm.com/docs/git-cherry-pick)

[cherry-picking explained](http://think-like-a-git.net/sections/rebase-from-the-ground-up/cherry-picking-explained.html)

http://stackoverflow.com/questions/9339429/what-does-cherry-picking-a-commit-with-git-mean

http://stackoverflow.com/questions/4024095/git-push-a-commit-in-two-branches

http://www.anexusit.com/blog/git-how-take-single-commit-one-branch-and-apply-it-another


## Keeping tracked files in a Git repository, but don't track changes

First change the file you do not want to be tracked and use the
following command:

    git update-index --assume-unchanged FILE_NAME

and if you want to track the changes again use this command:

    git update-index --no-assume-unchanged FILE_NAME

list all file is assume unchanged:

    git ls-files -v | grep '^[[:lower:]]'
    git ls-files -v | grep '^h'
    git ls-files -v | grep ^[a-z]
    git ls-files -v | grep -e "^[a-z]"

## Rename a branch

- [Rename the local branch](http://stackoverflow.com/questions/6591213/how-do-you-rename-the-local-branch)
- [Rename both local and remote Git repositories](http://stackoverflow.com/questions/1526794/rename-master-branch-for-both-local-and-remote-git-repositories?answertab=votes#tab-top)

- When rename a branch have pull request, so you must create new pull request with new branch.

## [Rename a file](http://git-scm.com/docs/git-mv)

`git mv <old_name> <new_name>`: rename a file, remember commit after renamed

`git mv --dry-run <old_name> <new_name>`: show what will happen but don't do it right now

`git mv -f oldfolder newfolder`: overwrite newfolder by oldfolder

## [Rename multiple files](http://stackoverflow.com/questions/9984722/git-rename-many-files-and-folders)

This should do the trick:

    for file in $(git ls-files | grep %filenamematch% | sed -e 's/\(%filenamematch%[^/]*\).*/\1/' | uniq); git mv $file $(echo $file | sed -e 's/%filenamematch%/%replacement%/')

To follow what this is doing, you'll need to understand piping with "|" and command substitution with "$(...)". These powerful shell constructs allow us to combine several commands to get the result we need. See [Pipelines](http://www.gnu.org/software/bash/manual/html_node/Pipelines.html) and [Command Substitution](http://wiki.bash-hackers.org/syntax/expansion/cmdsubst).


Here's what's going on in this one-liner:

1. `git ls-files`: This produces a list of files in the Git repository.
   It's similar to what you could get from `ls`, except it only outputs
   Git project files. Starting from this list ensures that nothing in
   your .git/ directory gets touched.

2. `| grep %filenamematch%`: We take the list from `git ls-files` and
   pipe it through grep to filter it down to only the file names
   containing the word or pattern we're looking for.

3. `| sed -e 's/\(%filenamematch%[^/]*\).*/\1/'`: We pipe these matches
   through [sed](http://ss64.com/bash/sed.html) (the stream editor),
   executing (-e) sed's s (substitute) command to chop off any / and
   subsequent characters after our matching directory (if it happens to
   be one).

4. `| uniq`: In cases where the match is a directory, now that we've
   chopped off contained directories and files, there could be many
   matching lines. We use uniq to make them all into one line.

5. `for file in ...`: The shell's ["for" command](http://www.gnu.org/software/bash/manual/html_node/Looping-Constructs.html) will iterate through all the items (file names) in the list. Each filename in turn, it assigns to the variable "$file" and then executes the command after the semicolon (;).

6. `sed -e 's/%filenamematch%/%replacement%/'`: We use [echo](http://ss64.com/bash/echo.html) to pipe each filename through sed, using it's substitute command again--this time to perform our pattern replacement on the filename.

7. `git mv`: We use this git command to mv the existing file ($file) to the new filename (the one altered by sed).

One way to understand this better would be to observe each of these
steps in isolation. To do that, run the commands below in your shell,
and observe the output. All of these are non-destructive, only producing
lists for your observation:

1. `git ls-files`

2. `git ls-files | grep %filenamematch%`

3. `git ls-files | grep %filenamematch% | sed -e 's/\(%filenamematch%[^/]*\).*/\1/'`

4. `git ls-files | grep %filenamematch% | sed -e 's/\(%filenamematch%[^/]*\).*/\1/' | uniq`

5. `for file in $(git ls-files | grep %filenamematch% | sed -e 's/\(%filenamematch%[^/]*\).*/\1/' | uniq); echo $file`

6. `for file in $(git ls-files | grep %filenamematch% | sed -e 's/\(%filenamematch%[^/]*\).*/\1/' | uniq); echo $file | sed -e 's/%filenamematch%/%replacement%/'`

### Example

Example: convert from use underscore to use dash

    IFS=$'\n'; for file in `git ls-files | grep "^MD.*_.*$"`; do git mv $file `echo $file | sed -e 's/_/-/g'`; done

## Clone http/https and pass user:pass by command line

`git clone https://username:password@github.com/username/repository.git`

`git clone http://tran.son:NtCavCAbdN0l@redmine.ig.webike.net/gitbucket/git/tran.son/vagrant_resources_GLOBAL.git`


## [Push/Pull to/from more than one repository](http://stackoverflow.com/questions/849308/pull-push-from-multiple-remote-locations)

    $ git remote set-url --add --push origin git://original/repo.git
    $ git remote set-url --add --push origin git://another/repo.git

    pushurl = git@bitbucket.org:samtron1412/map_tool.git
    pushurl = http://redmine.ig.webike.net/gitbucket/git/tran.son/map_tool.git

## [How to handle big repositories with git](http://blogs.atlassian.com/2014/05/handle-big-repositories-git/)

### Two categories of Big repositories

- They accumulate a very very long history (the project grows over a
  very long period of time and the baggage accumulates)
- They include huge binary assets that need to be tracked and paired
  together with code.
- Both of the above.

### Handling Repositories With Very Long History

#### Simple solution is a shallow clone

The first solution to a fast clone and to saving developers and systems
time and disk space is to perform a `shallow clone` using git. A shallow
clone allows you to clone a repository keeping only the latest `n`
commits of history.

How do you do it? Just use the `--depth` option, for example:


    git clone --depth <depth> remote-url

#### Partial solution is filter-branch

- Use `filter-repo` tool instead

For the huge repositories that have big binary cruft committed by
mistake or old assets not needed anymore a great solution is to use
filter-branch. The command allows to walk through the entire history of
the project filtering out, massaging, modifying, skipping files
according to predefined patterns. It is a very powerful tool in your git
arsenal. There are already helper scripts available to identify big
objects in your git repository, so that should be easy enough.

Sample usage of filter-branch (credit):

    git filter-branch --tree-filter 'rm -rf /path/to/spurious/asset/folder' HEAD


#### Alternative to shallow-clone: Clone only one branch

Since git 1.7.10, of April 2012 you can also limit the amount of history
you clone by cloning a single branch, like the following:

    git clone URL --branch branch_name --single-branch [folder]

### Handling Repositories With Huge Binary Assets

There are some [basic tweaks that improve the situation](http://thread.gmane.org/gmane.comp.version-control.git/146957/focus=147598), like running the garbage collection `git gc`, or tweaking the usage of delta commits for some binary types in `.gitattributes`.

But it’s important to reflect on the nature of you project’s binary
assets as the winning approach may vary. For example here are three
points to check (thanks to Stefan Saasen for the remarks):

- For binary files that change significantly – and not just some meta
  data headers – the delta compression is probably going to be useless
  so the suggestion is to turn delta off for those files to avoid the
  unnecessary delta compression work as part of the repack
- In the scenario above it’s likely that those files don’t zlib compress
  very well either so you could turn compression off with
  core.compression 0 or core.loosecompression 0; That’s a global setting
  that would negatively affect all the non-binary files that actually
  compress well so the suggestion makes sense if you split the binary
  assets in a separate repository.
- It’s important to remember that git gc turns the “duplicated” loose
  objects into a single pack file but again unless the files compress in
  any way that probably doesn’t make any significant difference in
  relation to the resulting pack file.
- Explore the tuning of core.bigFileThreshold. Anything larger than 512
  MiB won’t be delta compressed anyway – without having to set
  .gitattributes – so maybe that’s something worth tweaking.


http://stevelorek.com/how-to-shrink-a-git-repository.html

# Troubleshooting

## Checking which files are ignored as well as where the configuration is defined

- Show ignored files: `git status --ignored`
- Check where the configuration is defined:
    + `git check-ignore <file-path> -v`

## Common situations and solutions

- https://ohshitgit.com/

## No newline at end of file

- https://thoughtbot.com/blog/no-newline-at-end-of-file
- https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline
- https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings

## SSL cert self signed

Configuring projects do not verify certs: `git config http.sslVerify false`

# References

