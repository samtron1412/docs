## Chapter 1 - From zero to deploy
It's worth emphasizing that the goal of this book is not merely to teach Rails, but rather to **teach web development with Rails**, which means acquiring (or expanding) the skills needed to develop software for the World Wide Web.

In addition to Ruby on Rails, this skillset includes **HTML & CSS, databases, version control, testing, and deployment**. To accomplish this goal, the Ruby on Rails Tutorial takes an integrated approach: you will learn Rails by example by **building a substantial sample application from scratch**.

First chapter, we'll get started with Ruby on Rails by installing all the necessary software and by setting up our development environment (Section 1.2). Create first application and put it under version control system with Git (Section 1.3). Deploying it to production (Section 1.4).

Chapter 2, build a demo with **scaffolding**. And focus on interacting with this demo app through its URIs using a web browser.

The rest of tutorial focuses on developing a single large sample application, writing all the code from the scratch. We'll develop the sample app using **test-driven development** (TDD), getting started in Chapter 3 by creating **static pages** and then adding a **little dynamic content**. We'll take a quick detour in Chapter 4 to learn a little about the **Ruby language underlying Rails**. Then, in Chapter 5 through Chapter 9, we'll complete the foundation for the sample application by making a **site layout**, a **user data model**, and a **full registration and authentication system**. Finally, in Chapter 10 and Chapter 11 we'll add **microblogging** and **social features** to make a working example site.

### 1.1 - Introduction
#### 1.1.1 Comments for various readers
Begin [ruby](http://tryruby.org/), begin [rails](http://railsforzombies.org/).

Test-driven development is new for me, and the structured REST style favored by Rails.

#### 1.1.2 "Scaling" Rails
[you scale a site, not a framework](http://idleprocess.wordpress.com/2009/11/24/presentation-summary-high-performance-at-massive-scale-lessons-learned-at-facebook/).

### 1.2 - Up and running
#### 1.2.1 - Development environments
- IDEs: [RadRails](http://www.aptana.com/rails/) and [RubyMine](http://www.jetbrains.com/ruby/index.html)
- Text editors and command lines
    + Text editors: Sublime Text or Vim
    + Command lines

#### 1.2.2 - Ruby, RubyGems, Rails, and Git
- Install Git: `sudo apt-get install git`
- Install Ruby:
    + Install RVM:
        `$ curl -sSL https://get.rvm.io | bash -s stable`

        (If you have RVM installed, you should run

        `$ rvm get stable`

        to ensure that you have the latest version.)

		If you get the message “command not found”, you should run source on the rvm executable:

		`$ source ~/.rvm/scripts/rvm`

        You can then get Ruby set up by examining the requirements for installing it:

        `$ rvm requirements`

        Finally, installing Ruby 2.0.0:

        `$ rvm install 2.0.0`

    + GemSet:
        After installing Ruby, you should configure your system for the other software needed to run Rails applications. This typically involves installing gems, which are self-contained packages of Ruby code. Since gems with different version numbers sometimes conflict, it is often convenient to create separate gemsets, which are self-contained bundles of gems. For the purposes of this tutorial, I suggest creating a gemset called **railstutorial_rails_4_0**:

        `$ rvm use 2.0.0@railstutorial_rails_4_0 --create --default`

- Install RubyGems:
	Create file `.gemrc` at home folder to config no install ri and rdoc documents:

```
	install: --no-rdoc --no-ri
	update:  --no-rdoc --no-ri
```

- Install Rails:
    + `$ gem install rails --version 4.0.8`

#### 1.2.3 - The first application
    $ mkdir rails_projects
    $ cd rails_projects
    $ rails new first_app

A summary of the default Rails directory structure
**app/**    Core application (app) code, including models, views, controllers, and helpers
**app/assets**  is for assets that are owned by the application, such as custom images, JavaScript files or stylesheets.
**bin/**    Binary executable files
**config/** Application configuration
**db/** Database files
**doc/**    Documentation for the application
**lib/**    Library modules
**lib/assets**  is for your own libraries' code that doesn't really fit into the scope of the application or those libraries which are shared across applications.
**log/**    Application log files
**public/** Data accessible to the public (e.g., web browsers), such as error pages
**bin/rails**   A program for generating code, opening console sessions, or starting a local server
**test/**   Application tests (made obsolete by the spec/ directory in Section 3.1)
**tmp/**    Temporary files
**vendor/** Third-party code such as plugins and gems
**vendor/assets**   is for assets that are owned by outside entities, such as code for JavaScript plugins and CSS frameworks.
**README.rdoc** A brief description of the application
**Rakefile**    Utility tasks available via the rake command
**Gemfile** Gem requirements for this app
**Gemfile.lock**    A list of gems used to ensure that all copies of the app use the same gem versions
**config.ru**   A configuration file for Rack middleware
**.gitignore**  Patterns for files that should be ignored by Git

#### 1.2.4 - Bundler
After creating a new Rails application, the next step is to use Bundler to install and include the gems needed by the app. Bundler is run automatically (via bundle install) by the rails command, but in this section we’ll make some changes to the default application gems and run Bundler again.

Gemfile:

```
source 'https://rubygems.org'
ruby '2.0.0'
#ruby-gemset=railstutorial_rails_4_0

gem 'rails', '4.0.8'

group :development do
  gem 'sqlite3', '1.3.8'
end

gem 'sass-rails', '4.0.1'
gem 'uglifier', '2.1.1'
gem 'coffee-rails', '4.0.1'
gem 'jquery-rails', '3.0.4'
gem 'turbolinks', '1.1.1'
gem 'jbuilder', '1.0.2'

group :doc do
  gem 'sdoc', '0.3.20', require: false
end
```

    # Use Uglifier as compressor for JavaScript assets
    gem 'uglifier', '>= 1.3.0'

    # Use CoffeeScript for .js.coffee assets and views
    gem 'coffee-rails', '~> 4.0.0'

In other words, `the >= notation` always installs *the latest gem* when you run bundle install, whereas `the ~> 4.0.0 notation` only installs updated gems representing *minor point releases* (e.g., from 4.0.0 to 4.0.1), but not major point releases (e.g., from 4.0 to 4.1).

Unfortunately, experience shows that even minor point releases can break things, so for the Rails Tutorial we’ll err on the side of caution by including exact version numbers for virtually all gems. You are welcome to use the most up-to-date version of any gem, including using the ~> construction in the Gemfile (which I generally recommend for more **advanced users**), but be warned that this may cause the tutorial to act unpredictably.


    $ bundle update
    $ bundle install

#### 1.2.5 - rails server
(If your system complains about the lack of a JavaScript runtime, visit the [execjs page at GitHub](https://github.com/sstephenson/execjs) for a list of possibilities. I particularly recommend installing [Node.js](http://nodejs.org/).).

#### 1.2.6 - Model-View-Controller (MVC)
<figure>
  <figcaption style="text-align:center;">A schematic representation of the model-view-controller (MVC) architecture</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/mvc_schematic.png" alt="MVC" title="MVC">
</figure>

### 1.3 - Version control with Git
Version control systems allow us to **track changes to our project’s code**, **collaborate more easily**, and **roll back any inadvertent errors** (such as accidentally deleting files). Knowing how to use a version control system is a **required skill for every software developer**.

#### 1.3.1 - Installation and setup
##### First-time system setup
Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates. These variables can be stored in three different places:

- `/etc/gitconfig` file: Contains values for every user on the system and all their repositories. If you pass the option `--system` to git config, it reads and writes from this file specifically.
- `~/.gitconfig` file: Specific to your user. You can make Git read and write to this file specifically by passing the `--global` option.
- config file in the Git directory (that is, `.git/config`) of whatever repository you’re currently using: Specific to that single repository. *Each level overrides values in the previous level*, so values in .git/config trump those in /etc/gitconfig.

**Your identity**

    $ git config --global user.name "Your Name"
    $ git config --global user.email your.email@example.com

**Your editor**

    $ git config --global core.editor "subl -w"

**Checking your settings**

    git config --list
    git config user.name
    ...

##### First-time repository setup
First navigate to the root directory of the first app and initialize a new repository:

    $ git init

by default Git tracks the changes of all the files, but there are some files we don’t want to track. Git has a simple mechanism to ignore such files: simply include a file called `.gitignore` in the application root directory with some rules telling Git which files to ignore.

    # Ignore bundler config.
    /.bundle

    # Ignore the default SQLite database.
    /db/*.sqlite3
    /db/*.sqlite3-journal

    # Ignore all logfiles and tempfiles.
    /log/*.log
    /tmp

    # Ignore other unneeded files.
    database.yml
    doc/
    *.swp
    *~
    .project
    .DS_Store
    .idea
    .secret

#### 1.3.2 - Adding and committing
Add all the files

    $ git add .

To tell Git you want to keep the changes, use the commit command:

    $ git commit -m "Initialize repository"

By the way, you can see a list of your commit messages using the log command:

    $ git log

#### 1.3.3 - What good does Git do you?
When you delete some critical files, you can roll back by command:

    $ git checkout -f

#### 1.3.4 - GitHub
Putting a copy of your Git repository at GitHub serves two purposes: it’s a **full backup** of your code (including the full history of commits), and it makes any future **collaboration** much easier.

[GitHub SSh keys](https://help.github.com/articles/generating-ssh-keys)

Select none for README file and .gitignore, because rails is creates one.

After submitting the form, push up your first application as follows:

    $ git remote add origin https://github.com/<username>/first_app.git
    $ git push -u origin master

#### 1.3.5 - Branch, edit, commit, merge
In the process, we’ll see a first example of the branch, edit, commit, merge workflow that I recommend using with Git.

##### Branch
Git is incredibly good at making branches, which are *effectively copies of a repository where we can make (possibly experimental) changes without modifying the parent files*. In most cases, the parent repository is the `master` branch, and we can create a new topic branch by using `checkout` with the `-b` flag:

    $ git checkout -b modify-README
    Switched to a new branch 'modify-README'
    $ git branch
    master
    * modify-README

Here the second command, `git branch`, just lists all the local branches, and the asterisk `*` identifies which branch we’re currently on.

Note that `git checkout -b modify-README` both creates a new branch and switches to it.

The full value of branching only becomes clear when working on a project with **multiple developers**, but branches are helpful even for a single-developer tutorial such as this one. In particular, the *master branch is insulated from any changes we make to the topic branch*, so even if we really screw things up we can always *abandon the changes by checking out the master branch and deleting the topic branch*. We’ll see how to do this at the end of the section.

##### Edit
    $ git mv README.rdoc README.md
    $ subl README.md

```
# Ruby on Rails Tutorial: first application

This is the first application for the
[*Ruby on Rails Tutorial*](http://railstutorial.org/)
by [Michael Hartl](http://michaelhartl.com/).

Promgrammer [Thaison Tranhuynh](https://github.com/samtron1412)
```

##### Commit
Git provides the `-a` flag as a shortcut for the (very common) case of **committing all modifications to existing files** (or files created using git mv, which don’t count as new files to Git). **Be careful** about using the -a flag improperly; if you have added any new files to the project since the last commit, you still have to tell Git about them using `git add` first.

    $ git commit -a -m "Improve the README file"

##### Merge
Now that we’ve finished making our changes, we’re ready to merge the results **back into our master branch**:

```
$ git checkout master
Switched to branch 'master'
$ git merge modify-README
Updating 34f06b7..2c92bef
Fast forward
README.rdoc     |  243 --------------------------------------------------
README.md       |    5 +
2 files changed, 5 insertions(+), 243 deletions(-)
delete mode 100644 README.rdoc
create mode 100644 README.md
```

After you’ve merged in the changes, you can tidy up your branches by deleting the topic branch using `git branch -d` if you’re done with it:

    $ git branch -d modify-README

As mentioned above, it’s also possible to **abandon** your topic branch changes, in this case with `git branch -D`. Unlike the `-d` flag, the `-D` flag will delete the branch even though we **haven’t merged in the changes**.

##### Push
    $ git push

### 1.4 - Deploying
Deploying early and often allows us to **catch any deployment problems early in our development cycle**.

These include shared hosts or virtual private servers running [Phusion Passenger](http://www.modrails.com/) (a module for the Apache and Nginx21 web servers), full-service deployment companies such as [Engine Yard](http://engineyard.com/) and [Rails Machine](http://railsmachine.com/), and cloud deployment services such as [Engine Yard Cloud](http://cloud.engineyard.com/) and [Heroku](http://heroku.com/).

**Heroku** makes deploying Rails applications ridiculously easy - as long as your source code is under version control with Git. (This is yet another reason to follow the Git setup steps in Section 1.3 if you haven’t already.) The rest of this section is dedicated to deploying our first application to Heroku.

#### 1.4.1 - Heroku setup
Heroku uses the [PostgreSQL](http://www.postgresql.org/) database (pronounced “post-gres-cue-ell”, and often called “Postgres” for short), which means that we need to add the `pg` gem in the production environment to allow Rails to talk to Postgres:

    group :production do
      gem 'pg', '0.15.1'
      gem 'rails_12factor', '0.0.2'
    end

Note also the addition of the `rails_12factor` gem, which is used by Heroku to **serve static assets** such as images and stylesheets.

To install it, we run bundle install with a special flag:

    $ bundle install --without production

The `--without production` option prevents the **local installation** of any production gems, which in this case consists of `pg` and `rails_12factor`. (If Bundler complains about a readline error, try adding `gem 'rb-read\-line', '~> 0.4.2'` to your Gemfile.)

Because the only gems we’ve added are restricted to a production environment, **right now this command doesn’t actually install any additional local gems**, but it’s needed to update `Gemfile.lock` with the `pg` and `rails_12factor` gems and the specific Ruby version. We can commit the resulting change as follows:

    $ git commit -a -m "Update Gemfile.lock for Heroku"

The first step is to [sign up for Heroku](http://api.heroku.com/signup); after checking your email to complete the creation of your account, install the necessary Heroku software using the [Heroku Toolbelt](https://toolbelt.heroku.com/). Then use the `heroku` command to log in at the command line (you may have to exit and restart your terminal program first):

    $ heroku login

Finally, navigate back to your Rails project directory and use the heroku command to create a place on the Heroku servers for the sample app to live:

```
$ cd ~/rails_projects/first_app
$ heroku create
Created http://stormy-cloud-5881.herokuapp.com/ |
git@heroku.com:stormy-cloud-5881.herokuapp.com
Git remote heroku added
```

#### 1.4.2 - Heroku deployment, step one
To deploy the application, the first step is to use Git to push it up to Heroku:

    $ git push heroku master

#### 1.4.3 - Heroku deployment, step two
There is no step two! We’re already done. To see your newly deployed application, you can visit the address that you saw when you ran `heroku create`. You can also use an argument to the heroku command that automatically opens your browser with the right address:

    $ heroku open

Unfortunately, the resulting page is an error; as of Rails 4.0, for technical reasons the default Rails page doesn’t work on Heroku. The good news is that the error will go away (in the context of the full sample application) when we add a root route.
