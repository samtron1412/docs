# Chapter 3 - Mostly static pages
In this chapter, we will begin developing the **sample application** that will serve as our example throughout the rest of this tutorial. Although the sample app will eventually have **users**, **microposts**, and **a full login and authentication framework**, we will begin with a seemingly limited topic: **the creation of static pages**.

In fact, using Rails even for static pages yields a *distinct advantage*: we can easily **add just a small amount of dynamic content**. In this chapter we’ll learn how. Along the way, we’ll get our first taste of **automated testing**, which will help us be more confident that our code is correct. Moreover, having a good test suite will allow us to *refactor* our code with confidence, *changing its form without changing its function.*

**RSpec tests** will recur throughout the tutorial, so if you get stuck now I recommend forging ahead; you’ll be amazed how, after just a few more chapters, *initially inscrutable code* will suddenly look simple. (You might also consider the [RSpec course at Code School](http://mbsy.co/6VQ8l), which one reader has said answered a lot of his RSpec questions.)

Before getting started we need to create a new Rails project, this time called **sample_app**:

	$ cd ~/rails_projects
	$ rails new sample_app --skip-test-unit
	$ cd sample_app

Here the **--skip-test-unit** option to the rails command tells Rails not to generate a test directory associated with the default **Test::Unit** framework. This is not because we won’t be writing tests; on the contrary, starting in Section 3.2 we will be using an alternate testing framework called **RSpec** to write a thorough test suite.

Next step is to use a text editor to update the **Gemfile** with the gems needed by our application. On the other hand, for the sample application we’ll also need two gems we didn’t need before: *the gem for RSpec and the gem for the RSpec library specific to Rails*.

	source 'https://rubygems.org'
	ruby '2.0.0'
	#ruby-gemset=railstutorial_rails_4_0

	gem 'rails', '4.0.8'
	gem 'bootstrap-sass', '2.3.2.0'
	gem 'sprockets', '2.11.0'
	gem 'bcrypt-ruby', '3.1.2'
	gem 'faker', '1.1.2'
	gem 'will_paginate', '3.0.4'
	gem 'bootstrap-will_paginate', '0.0.9'

	group :development, :test do
	  gem 'sqlite3', '1.3.8'
	  gem 'rspec-rails', '2.13.1'
	  # The following optional lines are part of the advanced setup.
	  # gem 'guard-rspec', '2.5.0'
	  # gem 'spork-rails', '4.0.0'
	  # gem 'guard-spork', '1.5.0'
	  # gem 'childprocess', '0.3.6'
	end

	group :test do
	  gem 'selenium-webdriver', '2.35.1'
	  gem 'capybara', '2.1.0'
	  gem 'factory_girl_rails', '4.2.0'
	  gem 'cucumber-rails', '1.4.0', :require => false
	  gem 'database_cleaner', github: 'bmabey/database_cleaner'

	  # Uncomment this line on OS X.
	  # gem 'growl', '1.0.3'

	  # Uncomment these lines on Linux.
	  # gem 'libnotify', '0.8.0'

	  # Uncomment these lines on Windows.
	  # gem 'rb-notifu', '0.0.4'
	  # gem 'wdm', '0.1.0'
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

	group :production do
	  gem 'pg', '0.15.1'
	  gem 'rails_12factor', '0.0.2'
	end

This includes **rspec-rails** in a *development environment* so that we have access to RSpec-specific generators, and it includes it in *test mode* in order to run the tests. We don’t have to install RSpec itself because it is a dependency of rspec-rails and will thus be installed automatically. We also include the [Capybara](https://github.com/jnicklas/capybara) gem, which allows us to *simulate a user’s interaction with the sample application using a natural English-like syntax*, together with [Selenium](http://docs.seleniumhq.org/projects/webdriver/), one of Capybara’s dependencies.1 As in [Chapter 2](#chapter-2-a-demo-app), we also must include the PostgreSQL and static assets gems in production for deployment to Heroku

To install and include the new gems, we run **bundle install**:

	$ bundle install --without production
	$ bundle update

Because the sample application is shared as a public repository, it’s important to update the so-called **secret token** used by Rails to *protect session variables* so that it is dynamically generated rather than hard-coded (Listing 3.2). (The code in Listing 3.2 is fairly advanced for so early in the tutorial, but because it’s a **potentially serious security issue** I feel it’s important to include it even at this early stage.) Be sure to use the augmented **.gitignore** file so that the **.secret** key isn’t exposed in your repository.

**Note**: If your app is missing **secret_token.rb** and has **secrets.yml** instead, it probably means you installed Rails 4.1 by mistake. In this case, uninstall Rails using gem uninstall rails and then reinstall it.

	# Be sure to restart your server when you modify this file.

	# Your secret key is used for verifying the integrity of signed cookies.
	# If you change this key, all old signed cookies will become invalid!

	# Make sure the secret is at least 30 characters and all random,
	# no regular words or you'll be exposed to dictionary attacks.
	# You can use `rake secret` to generate a secure secret key.

	# Make sure your secret_key_base is kept private
	# if you're sharing your code publicly.
	require 'securerandom'

	def secure_token
	  token_file = Rails.root.join('.secret')
	  if File.exist?(token_file)
	    # Use the existing token.
	    File.read(token_file).chomp
	  else
	    # Generate a new token and store it in token_file.
	    token = SecureRandom.hex(64)
	    File.write(token_file, token)
	    token
	  end
	end

	SampleApp::Application.config.secret_key_base = secure_token

Next, we need to configure Rails to use RSpec in place of **Test::Unit**. This can be accomplished with **rails generate rspec:install**:

	$ rails generate rspec:install

initialize the Git repository:

	$ git init
	$ git add .
	$ git commit -m "Initial commit"

Improve README file

	$ git mv README.rdoc README.md
	$ git commit -am "Improve the README"

Push to GitHub

	$ git remote add origin https://github.com/<username>/sample_app.git
	$ git push -u origin master

Deploy to Heroku

	$ heroku create
	$ git push heroku master
	$ heroku run rake db:migrate

As you proceed through the rest of the book, I recommend pushing and deploying the application **regularly**:

	$ git push
	$ git push heroku
	$ heroku run rake db:migrate

This provides remote backups and lets you *catch any production errors as soon as possible*. If you run into problems at Heroku, make sure to take a look at the production logs to try to diagnose the problem:

	$ heroku logs

## 3.1 - Static pages
creating a set of Rails actions and views containing (for now) only static HTML. in essence, a controller is a container for a group of (possibly dynamic) web pages. In this section, we’ll be working mainly in the *app/controllers* and **app/views** directories.

Open project in editor:

	$ cd ~/rails_projects/sample_app
	$ <editor name> . (eg. subl .)

To get started with static pages, when using Git, it’s a *good practice* to do our work on a separate topic branch rather than the master branch. If you’re using Git for version control, you should run the following command:

	$ git checkout -b static-pages

Rails comes with a script for making controllers called **generate**; all it needs to work its magic is the controller’s name. Since we’ll be making a controller to handle static pages, we’ll call it the *StaticPages* controller. We’ll also plan to make actions for a *Home* page, a *Help* page, and an *About* page. The generate script takes an optional list of actions, so we’ll include two of the initial actions directly on the command line:

	Listing 3.4:
	$ rails generate controller StaticPages home help --no-test-framework

Here we’ve used the option **--no-test-framework** to *suppress the generation of the default RSpec tests*, which we won’t be using. Instead, we’ll *create the tests by hand* starting in Section 3.2. We’ve also intentionally left off the **about** action from the command line arguments in Listing 3.4 so that we can see how to add it using **test-driven development**, or **TDD** (Section 3.2).

In Listing 3.4, note that we have passed the controller name as so-called [CamelCase](https://en.wikipedia.org/wiki/CamelCase), which leads to the creation of a controller file written in [snake case](https://en.wikipedia.org/wiki/Snake_case), so that a controller called **StaticPages** yields a file called **static_pages_controller.rb**. This is merely a convention, and in fact using snake case at the command line also works: the command behind

	$ rails generate controller static_pages ...

also generates a controller called **static_pages_controller.rb**. Because Ruby uses *CamelCase for class names* (Section 4.4), my preference is to refer to controllers using their CamelCase names, but this is a matter of taste. (Since Ruby *filenames typically use snake case*, the Rails generator converts CamelCase to snake case using the [underscore](http://api.rubyonrails.org/classes/ActiveSupport/Inflector.html#method-i-underscore) method.)

By the way, if you ever make a mistake when generating code, it’s useful to know how to *reverse the process*. See Box 3.2 for some techniques on how to *undo things in Rails*.

	$ rails generate controller FooBars baz quux
	$ rails destroy  controller FooBars baz quux

	$ rails generate model Foo bar:string baz:integer
	$ rails destroy model Foo

	$ rake db:migrate
	$ rake db:rollback (undo a single migration step)
	$ rake db:migrate VERSION=0 (go all the way back to the beginning)

With these techniques in hand, we are well-equipped to recover from *the inevitable development* [snafus](http://en.wikipedia.org/wiki/SNAFU).

The StaticPages controller generation in Listing 3.4 automatically updates the routes file, called **config/routes.rb**, which Rails uses to *find the correspondence between URLs and web pages*. The **config** directory is where Rails collects files needed for the application configuration.

**GET** is the most common HTTP operation, used for reading data on the web; it just means “get a page”, and every time you visit a site like google.com or wikipedia.org your browser is submitting a GET request. **POST** is the next most common operation; it is the request sent by your browser when you *submit a form*. In Rails applications, POST requests are typically used for *creating things* (although HTTP also allows POST to perform updates); for example, the POST request sent when you submit a registration form creates a new user on the remote site. The other two verbs, **PATCH** and **DELETE**, are designed for *updating* and *destroying* things on the remote server.

	Listing 3.6:
	class StaticPagesController < ApplicationController

	  def home
	  end

	  def help
	  end
	end

In plain Ruby, these methods would simply do nothing. In Rails, the situation is different—StaticPagesController is a Ruby class, but because it inherits from ApplicationController the behavior of its methods is specific to Rails: when visiting the URL `/static_pages/home`, Rails looks in the StaticPages controller and *executes the code* in the home action, and then *renders the view* corresponding to the action. In the present case, the home action is empty, so all visiting `/static_pages/home` does is render the view.

Views

	Listing 3.7:
	<h1>StaticPages#home</h1>
	<p>Find me in app/views/static_pages/home.html.erb</p>

	Listing 3.8:
	<h1>StaticPages#help</h1>
	<p>Find me in app/views/static_pages/help.html.erb</p>

Rails views can simply contain static HTML. In the remainder of this chapter, we’ll add some custom content to the Home and Help pages, and then add in the About page.

Before moving on, if you’re using Git it’s a good idea to add the files for the StaticPages controller to the repository:

	$ git add .
	$ git commit -m "Add a StaticPages controller"

## 3.2 - Our first tests
The Rails Tutorial takes *an intuitive approach* to testing that *emphasizes the behavior* of the application rather than *its precise implementation*, a variant of test-driven development (TDD) known as behavior-driven development (BDD). Our main tools will be **integration tests** (starting in this section) and **unit tests** (starting in Chapter 6).

Integration tests, known as *request specs* in the context of RSpec, allow us to *simulate the actions of a user interacting with our application using a web browser*. Together with the *natural-language syntax* provided by *Capybara*, integration tests provide a powerful method to *test our application’s functionality without having to manually check each page with a browser*.

The defining quality of TDD is **writing tests first, before the application code**. Initially, this might take some getting used to, but the benefits are significant. By writing a failing test first and then implementing the application code to get it to pass, we increase our confidence that the test is actually covering the functionality we think it is.

Moreover, the **fail-implement-pass development cycle** induces a [flow state](http://en.wikipedia.org/wiki/Flow_(psychology)), leading to *enjoyable coding* and *high productivity*. Finally, the tests act as a *client* for the application code, often leading to more *elegant software designs*.

It’s important to understand that TDD is **not always the right tool for the job**: there’s no reason to *dogmatically insist* that tests always should be written first, that they should cover every single feature, or that there should necessarily be any tests at all. For example, when you *aren’t at all sure how to solve a given programming problem*, it’s often useful to skip the tests and write only application code, just to get a sense of what the solution will look like. (In the language of [Extreme Programming](http://en.wikipedia.org/wiki/Extreme_Programming) (XP), this exploratory step is called a spike.) Once you see the general shape of the solution, you can then use TDD to implement a *more polished version*.

In this section, we’ll be running the tests using the **rspec** command supplied by the RSpec gem. This practice is *straightforward but not ideal*, and if you are a more advanced user I suggest setting up your system as described in [Section 3.6](#36-advanced-setup).

### 3.2.1 - Test-driven development
In test-driven development, we first write a *failing test*, represented in many testing tools by the color *red*. We then *implement code to get the test to pass*, represented by the color *green*. Finally, if necessary, we *refactor* the code, changing its form (by eliminating duplication, for example) *without changing its function*. This cycle is known as **“Red, Green, Refactor”**.

We’ll begin by adding some content to the Home page using test-driven development, including a top-level heading (**<h1>**) with the content **Sample App**. The first step is to generate an integration test (request spec) for our static pages:

	$ rails generate integration_test static_pages
	      invoke  rspec
	      create    spec/requests/static_pages_spec.rb

This creates the **static_pages_spec.rb** in the **spec/requests** directory. As with most generated code, the result is not pretty, so let’s open **static_pages_spec.rb** with a text editor and replace it with the contents of Listing 3.9.

	Listing 3.9:
	require 'spec_helper'

	describe "Static pages" do

	  describe "Home page" do

	    it "should have the content 'Sample App'" do
	      visit '/static_pages/home'
	      expect(page).to have_content('Sample App')
	    end
	  end
	end

The code in Listing 3.9 is pure Ruby, but even if you’ve studied Ruby before it might not look familiar. This is because RSpec uses the *general malleability of Ruby* to define a **domain-specific language** (DSL) built just for testing. The important point is that you do not need to understand RSpec’s syntax to be able to use RSpec. It may seem like magic at first, but RSpec and Capybara are designed to *read more or less like English*, and if you follow the examples in this tutorial you’ll pick it up fairly quickly.

The first line indicates that we are describing the Home page. This description is just a string, and it can be anything you want; RSpec doesn’t care, but you and other human readers probably do. To get the test to run properly, we have to add a line to the **spec_helper.rb** file:

	Listing 3.10:
	# This file is copied to spec/ when you run 'rails generate rspec:install'
	.
	.
	.
    RSpec.configure do |config|
	  .
	  .
	  .
	  config.include Capybara::DSL 		# add this line to spec_helper.rb
	end

To actually run the test, we have several options, including some convenient but rather advanced tools discussed in [Section 3.6](#36-advanced-setup). For now, we’ll use the **rspec** command at the command line (executed with **bundle exec** to ensure that RSpec runs in the environment specified by our **Gemfile**)

	$ bundle exec rspec spec/requests/static_pages_spec.rb

This yields a failing test. To get the test to pass, we’ll replace the default Home page test with the HTML:

	Listing 3.11:
	<h1>Sample App</h1>
	<p>
	  This is the home page for the
	  <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	  sample application.
	</p>

Re-run test and the passing test appears.

Adding code test for Help page:

	Listing 3.12:
	require 'spec_helper'

	describe "Static pages" do

	  describe "Home page" do

	    it "should have the content 'Sample App'" do
	      visit '/static_pages/home'
	      expect(page).to have_content('Sample App')
	    end
	  end

	  describe "Help page" do

	    it "should have the content 'Help'" do
	      visit '/static_pages/help'
	      expect(page).to have_content('Help')
	    end
	  end
	end

Code of new Help page:

	Listing 3.13:
	<h1>Help</h1>
	<p>
	  Get help on the Ruby on Rails Tutorial at the
	  <a href="http://railstutorial.org/help">Rails Tutorial help page</a>.
	  To get help on this sample app, see the
	  <a href="http://railstutorial.org/book">Rails Tutorial book</a>.
	</p>

### 3.2.2 - Adding a page
Having seen test-driven development in action in a simple example, we’ll use the same technique to accomplish the slightly more complicated task of *adding a new page, namely*, the **About** page that we intentionally left off in Section 3.1. By writing a test and running RSpec at each step, we’ll see how TDD can guide us through the development of our application code.

**Red**

We’ll get to the Red part of the Red-Green cycle by writing a failing test for the About page.

	Listing 3.14:
	require 'spec_helper'

	describe "Static pages" do

	  describe "Home page" do

	    it "should have the content 'Sample App'" do
	      visit '/static_pages/home'
	      expect(page).to have_content('Sample App')
	    end
	  end

	  describe "Help page" do

	    it "should have the content 'Help'" do
	      visit '/static_pages/help'
	      expect(page).to have_content('Help')
	    end
	  end

	  describe "About page" do

	    it "should have the content 'About Us'" do
	      visit '/static_pages/about'
	      expect(page).to have_content('About Us')
	    end
	  end
	end

**Green**

Recall from Section 3.1 that we can *generate a static page in Rails by creating an action and corresponding view with the page’s name*. In our case, the About page will first need an action called about in the StaticPages controller. Having written a failing test, we can now be confident that, in getting it to pass, we will actually have created a working About page.

Follow hint at Rspec test. First add route to routes.rb. Create new action at StaticPagesController. Create new view:

	Listing 3.17:
	<h1>About Us</h1>
	<p>
	  The <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	  is a project to make a book and screencasts to teach web development
	  with <a href="http://rubyonrails.org/">Ruby on Rails</a>. This
	  is the sample application for the tutorial.
	</p>

**Refactor**
Now that we’ve gotten to Green, we are free to refactor our code with confidence. Oftentimes code will start to “smell”, meaning that it gets *ugly*, *bloated*, or *filled with repetition*. The computer doesn’t care, of course, but humans do, so it is important to keep the code base clean by refactoring frequently. Having a good test suite is *an invaluable tool* in this *regard*, as it dramatically lowers the probability of introducing bugs while refactoring.

## 3.3 - Slightly dynamic pages
### 3.3.1 - Testing a title change
You may have noticed that the rails new command already created a **layout file**. We’ll learn its purpose shortly, but for now you should rename it before proceeding:

    $ mv app/views/layouts/application.html.erb foobar   # temporary change

Adding new tests for each of our three static pages, gives us our new StaticPages test (Listing 3.19). Note that there is considerable repetition here, which we will eliminate in Section 5.3.4.


    Listing 3.19:
    require 'spec_helper'

    describe "Static pages" do

      describe "Home page" do

        it "should have the content 'Sample App'" do
          visit '/static_pages/home'
          expect(page).to have_content('Sample App')
        end

        it "should have the title 'Home'" do
          visit '/static_pages/home'
          expect(page).to have_title("Ruby on Rails Tutorial Sample App | Home")
        end
      end

      describe "Help page" do

        it "should have the content 'Help'" do
          visit '/static_pages/help'
          expect(page).to have_content('Help')
        end

        it "should have the title 'Help'" do
          visit '/static_pages/help'
          expect(page).to have_title("Ruby on Rails Tutorial Sample App | Help")
        end
      end

      describe "About page" do

        it "should have the content 'About Us'" do
          visit '/static_pages/about'
          expect(page).to have_content('About Us')
        end

        it "should have the title 'About Us'" do
          visit '/static_pages/about'
          expect(page).to have_title("Ruby on Rails Tutorial Sample App | About Us")
        end
      end
    end

You should run:

    $ bundle exec rspec spec/requests/static_pages_spec.rb

to verify that our code is now Red.

### 3.3.2 - Passing title tests
The new Home page:

    Listing 3.20:
    <!DOCTYPE html>
    <html>
      <head>
        <title>Ruby on Rails Tutorial Sample App | Home</title>
      </head>
      <body>
        <h1>Sample App</h1>
        <p>
          This is the home page for the
          <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
          sample application.
        </p>
      </body>
    </html>

new Help page:

    Listing 3.21:
    <!DOCTYPE html>
    <html>
      <head>
        <title>Ruby on Rails Tutorial Sample App | Help</title>
      </head>
      <body>
        <h1>Help</h1>
        <p>
          Get help on the Ruby on Rails Tutorial at the
          <a href="http://railstutorial.org/help">Rails Tutorial help page</a>.
          To get help on this sample app, see the
          <a href="http://railstutorial.org/book">Rails Tutorial book</a>.
        </p>
      </body>
    </html>

new About page:

	Listing 3.22:
	<!DOCTYPE html>
	<html>
	  <head>
	    <title>Ruby on Rails Tutorial Sample App | About Us</title>
	  </head>
	  <body>
	    <h1>About Us</h1>
	    <p>
	      The <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	      is a project to make a book and screencasts to teach web development
	      with <a href="http://rubyonrails.org/">Ruby on Rails</a>. This
	      is the sample application for the tutorial.
	    </p>
	  </body>
	</html>

verify all work by:

	$ bundle exec rspec spec/requests/static_pages_spec.rb

### 3.3.3 - Embedded Ruby
they suffer from terrible duplication:

- The page titles are almost (but not quite) exactly the same.
- “Ruby on Rails Tutorial Sample App” is common to all three titles.
- The entire HTML skeleton structure is repeated on each page.

This repeated code is a violation of the important “**Don’t Repeat Yourself**” (DRY) principle; in this section and the next we’ll “DRY out our code” by removing the repetition.

new Home page code with embedded ruby:

	Listing 3.23:
	<% provide(:title, 'Home') %>
	<!DOCTYPE html>
	<html>
	  <head>
	    <title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
	  </head>
	  <body>
	    <h1>Sample App</h1>
	    <p>
	      This is the home page for the
	      <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	      sample application.
	    </p>
	  </body>
	</html>

(The distinction between the two types of embedded Ruby is that `<% ... %>` executes the code inside, while `<%= ... %>` executes it and inserts the result into the template.)

verify all work by:

	$ bundle exec rspec spec/requests/static_pages_spec.rb

new Help page with embedded ruby:

	Listing 3.24:
	<% provide(:title, 'Help') %>
	<!DOCTYPE html>
	<html>
	  <head>
	    <title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
	  </head>
	  <body>
	    <h1>Help</h1>
	    <p>
	      Get help on the Ruby on Rails Tutorial at the
	      <a href="http://railstutorial.org/help">Rails Tutorial help page</a>.
	      To get help on this sample app, see the
	      <a href="http://railstutorial.org/book">Rails Tutorial book</a>.
	    </p>
	  </body>
	</html>

new About page with bedded ruby:

	Listing 3.25:
	<% provide(:title, 'About Us') %>
	<!DOCTYPE html>
	<html>
	  <head>
	    <title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
	  </head>
	  <body>
	    <h1>About Us</h1>
	    <p>
	      The <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	      is a project to make a book and screencasts to teach web development
	      with <a href="http://rubyonrails.org/">Ruby on Rails</a>. This
	      is the sample application for the tutorial.
	    </p>
	  </body>
	</html>

### 3.3.4 - Eliminating duplication with layouts
Our pages are identical in structure, including the contents of the title tag, with the sole exception of the material inside the body tag.

In order to factor out this common structure, Rails comes with a special *layout file* called **application.html.erb**, which we renamed in Section 3.3.1 and which we’ll now restore:

	$ mv foobar app/views/layouts/application.html.erb

content of layout file: we add one line of title page

	Listing 3.26:
	<!DOCTYPE html>
	<html>
	<head>
	  <title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
	  <%= stylesheet_link_tag    "application", media: "all",
	                                            "data-turbolinks-track" => true %>
	  <%= javascript_include_tag "application", "data-turbolinks-track" => true %>
	  <%= csrf_meta_tags %>
	</head>
	<body>

	<%= yield %>

	</body>
	</html>

this line we added to create title page change:

	<title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>

note this line:

	<%= yield %>

it converts the contents of **home.html.erb** to HTML and then inserts it in place of **<%= yield %>**.

default Rails layout includes additional line:

	<%= stylesheet_link_tag ... %>
	<%= javascript_include_tag "application", ... %>
	<%= csrf_meta_tags %>

This code arranges to include the application **stylesheet** and **JavaScript**, which are part of the **asset pipeline** (Section 5.2.1), together with the Rails method **csrf_meta_tags**, which prevents [cross-site request forgery](http://en.wikipedia.org/wiki/Cross-site_request_forgery) (CSRF), a type of malicious web attack.

new Home page after apply new layout:

	Listing 3.27:
	<% provide(:title, 'Home') %>
	<h1>Sample App</h1>
	<p>
	  This is the home page for the
	  <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	  sample application.
	</p>

new Help page:

	Listing 3.28:
	<% provide(:title, 'Help') %>
	<h1>Help</h1>
	<p>
	  Get help on the Ruby on Rails Tutorial at the
	  <a href="http://railstutorial.org/help">Rails Tutorial help page</a>.
	  To get help on this sample app, see the
	  <a href="http://railstutorial.org/book">Rails Tutorial book</a>.
	</p>

new About page:

	Listing 3.29:
	<% provide(:title, 'About Us') %>
	<h1>About Us</h1>
	<p>
	  The <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	  is a project to make a book and screencasts to teach web development
	  with <a href="http://rubyonrails.org/">Ruby on Rails</a>. This
	  is the sample application for the tutorial.
	</p>

verify code by:

	$ bundle exec rspec spec/requests/static_pages_spec.rb

## 3.4 - Conclusion
make a commit indicating that we’ve reached a stopping point:

	$ git add .
	$ git commit -m "Finish static pages"

Then merge the changes back into the master branch:

	$ git checkout master
	$ git merge static-pages

push your code up to a remote repository:

	$ git push

deploy the updated application to Heroku"

	$ git push heroku

## 3.5 - Exercises
### Write a Contact page
first write a test for the existence of a page at the URL **/static_pages/contact** by testing for the title “Ruby on Rails Tutorial Sample App | Contact”. Get your test to pass by filling the Contact page with the content:

	Listing 3.30:
	<% provide(:title, 'Contact') %>
	<h1>Contact</h1>
	<p>
	  Contact Ruby on Rails Tutorial about the sample app at the
	  <a href="http://railstutorial.org/contact">contact page</a>.
	</p>

### Edit RSpec file to DRY code
use let **function** and **string interpolation**:

	Listing 3.31:
	require 'spec_helper'

	describe "Static pages" do

	  let(:base_title) { "Ruby on Rails Tutorial Sample App" }

	  describe "Home page" do

	    it "should have the content 'Sample App'" do
	      visit '/static_pages/home'
	      expect(page).to have_content('Sample App')
	    end

	    it "should have the title 'Home'" do
	      visit '/static_pages/home'
	      expect(page).to have_title("#{base_title} | Home")
	    end
	  end

	  describe "Help page" do

	    it "should have the content 'Help'" do
	      visit '/static_pages/help'
	      expect(page).to have_content('Help')
	    end

	    it "should have the title 'Help'" do
	      visit '/static_pages/help'
	      expect(page).to have_title("#{base_title} | Help")
	    end
	  end

	  describe "About page" do

	    it "should have the content 'About Us'" do
	      visit '/static_pages/about'
	      expect(page).to have_content('About Us')
	    end

	    it "should have the title 'About Us'" do
	      visit '/static_pages/about'
	      expect(page).to have_title("#{base_title} | About Us")
	    end
	  end

	  describe "Contact page" do

	    it "should have the content 'Contact'" do
	      visit '/static_pages/contact'
	      expect(page).to have_content('Contact')
	    end

	    it "should have the title 'Contact'" do
	      visit '/static_pages/contact'
	      expect(page).to have_title("#{base_title} | Contact")
	    end
	  end
	end

### Config PostgreSQL at local
Follow the [Heroku instructions for local PostgreSQL](http://devcenter.heroku.com/articles/local-postgresql) installation to install the PostgreSQL database on your local system. Update your **Gemfile** to eliminate the **sqlite3** gem and use the **pg** gem exclusively.

Note for install **pg** gem, before bundle install or update, install right package:

	sudo apt-get install postgresql
	sudo apt-get install libpq-dev

see [install](http://www.postgresql.org/download/) page to know specific step for each system.

Change the postgresql configuration to solve this error

	FATAL: Peer authentication failed for user

`sudo nano /etc/postgresql/9.1/main/pg_hba.conf`

Replace **local peer** with **local md5** in the file. Then *reload postgresql* to apply the change.

`sudo /etc/init.d/postgresql reload`

Set up a user that is the same as my Ubuntu log-in

	$ sudo su postgres -c psql
	postgres=# CREATE ROLE <username> SUPERUSER LOGIN;
	postgres=# \q

new Gemfile:

	# Remove gem 'sqlite3'
	gem 'pg'

Modify **database.yml** in app directory

	development:
	  adapter: postgresql
	  encoding: unicode
	  database: appname_development
	  pool: 5
	  timeout: 5000
	  username: <username>
	  password:

	test:
	  adapter: postgresql
	  encoding: unicode
	  database: appname_test
	  pool: 5
	  timeout: 5000
	  username: <username>
	  password:

Run bundle install

	$ bundle install

Create databases and migrations

	$ rake db:create:all
	$ rake db:migrate

## 3.6 - Advanced setup
In this section, we’ll first discuss a method to eliminate the necessity of typing **bundle exec**, and then set up testing to automate the running of the test suite using **Guard** (Section 3.6.2) and, optionally, **Spork** (Section 3.6.3). Finally, we’ll mention a method for *running tests directly inside Sublime Text*, a technique especially useful when used in concert with Spork.

### 3.6.1 - Eliminating bundle exec
**RVM Bundler integration**
The first and preferred method is to use RVM, which includes Bundler integration as of version 1.11. You can verify that you have a sufficiently up-to-date version of RVM as follows:

	$ rvm get stable
	$ rvm -v

As long as the version number is 1.11.x or greater, installed gems will automatically be executed in the proper Bundler environment, so that you can write (for example)

	$ rspec spec/

and omit the leading **bundle exec**.

### 3.6.2 - Automated test with Guard
One annoyance associated with using the rspec command is having to switch to the command line and run the tests by hand. A second annoyance, the slow start-up time of the test suite, is addressed in Section 3.6.3.

In this section, we’ll show how to use [Guard](https://github.com/guard/guard) to automate the running of the tests. Guard monitors changes in the filesystem so that, for example, when we change the **static_pages_spec.rb** file *only those tests get run*. Even better, we can configure Guard so that when, say, the **home.html.erb** file is modified, the **static_pages_spec.rb** automatically runs.

First we add **guard-rspec** to the **Gemfile**:

	group :development, :test do
	  gem 'rspec-rails', '2.13.1'
	  gem 'guard-rspec', '2.5.0'
	end

Be sure to uncomment the lines in the test group relevant for your system:

	group :test do
	  gem 'selenium-webdriver', '2.35.1'
	  gem 'capybara', '2.1.0'

	  # Uncomment this line on OS X.
	  # gem 'growl', '1.0.3'

	  # Uncomment these lines on Linux.
	  # gem 'libnotify', '0.8.0'

	  # Uncomment these lines on Windows.
	  # gem 'rb-notifu', '0.0.4'
	  # gem 'wdm', '0.1.0'
	end

We next install the gems by running bundle install:

	$ bundle install

Then initialize Guard so that it works with RSpec:

	$ bundle exec guard init rspec
	Writing new Guardfile to /Users/mhartl/rails_projects/sample_app/Guardfile
	rspec guard added to Guardfile, feel free to edit it

Now edit the resulting **Guardfile** so that Guard will run the right tests when the *integration tests* and *views* are updated:

	Listing 3.35:
	require 'active_support/inflector'

	guard 'rspec', all_after_pass: false do
	  .
	  .
	  .
	  watch('config/routes.rb')
	  # Custom Rails Tutorial specs
	  watch(%r{^app/controllers/(.+)_(controller)\.rb$}) do |m|
	    ["spec/routing/#{m[1]}_routing_spec.rb",
	     "spec/#{m[2]}s/#{m[1]}_#{m[2]}_spec.rb",
	     "spec/acceptance/#{m[1]}_spec.rb",
	     (m[1][/_pages/] ? "spec/requests/#{m[1]}_spec.rb" :
	                       "spec/requests/#{m[1].singularize}_pages_spec.rb")]
	  end
	  watch(%r{^app/views/(.+)/}) do |m|
	    (m[1][/_pages/] ? "spec/requests/#{m[1]}_spec.rb" :
	                      "spec/requests/#{m[1].singularize}_pages_spec.rb")
	  end
	  watch(%r{^app/controllers/sessions_controller\.rb$}) do |m|
	    "spec/requests/authentication_pages_spec.rb"
	  end
	  .
	  .
	  .
	end

Here the line

	guard 'rspec', all_after_pass: false do

ensures that Guard doesn’t run all the tests after a failing test passes (to speed up the Red-Green-Refactor cycle).

We can now start guard as follows:

	$ bundle exec guard

By the way, if you get a Guard error complaining about the *absence of* a **spec/routing** directory, you can fix it by creating an empty one:

	$ mkdir spec/routing

### 3.6.3 - Speeding up tests with Spork
When running bundle exec rspec, you may have noticed that it takes several seconds just to start running the tests, but once they start running they finish quickly. This is because each time RSpec runs the tests it has to *reload the entire Rails environment*.

The [Spork test server](http://github.com/sporkrb/spork) aims to solve this problem. Spork loads the environment **once**, and then maintains a pool of processes for running future tests. Spork is particularly useful when combined with Guard.

The first step is to add the **spork** gem dependency to the **Gemfile**:

	Listing 3.36:
	group :development, :test do
	  .
	  .
	  .
	  gem 'spork-rails', '4.0.0'
	  gem 'guard-spork', '1.5.0'
	  gem 'childprocess', '0.3.6'
	end

Then install Spork using bundle install:

	$ bundle install

Next, bootstrap the Spork configuration:

	$ bundle exec spork --bootstrap

Now we need to edit the *RSpec configuration file*, located in **spec/spec_helper.rb**, so that the environment gets loaded in a *prefork* block, which arranges for it to be loaded only *once*

	Listing 3.37: Adding environment loading to the Spork.prefork block.
	require 'rubygems'
	require 'spork'

	Spork.prefork do
	  ENV["RAILS_ENV"] ||= 'test'
	  require File.expand_path("../../config/environment", __FILE__)
	  require 'rspec/rails'
	  require 'rspec/autorun'

	  # Requires supporting ruby files with custom matchers and macros, etc,
	  # in spec/support/ and its subdirectories.
	  Dir[Rails.root.join("spec/support/**/*.rb")].each {|f| require f}

	  # Checks for pending migrations before tests are run.
	  # If you are not using ActiveRecord, you can remove this line.
	  ActiveRecord::Migration.check_pending! if defined?(ActiveRecord::Migration)

	  RSpec.configure do |config|
	    # ## Mock Framework
	    #
	    # If you prefer to use mocha, flexmock or RR, uncomment the appropriate line:
	    #
	    # config.mock_with :mocha
	    # config.mock_with :flexmock
	    # config.mock_with :rr

	    # Remove this line if you're not using ActiveRecord or ActiveRecord fixtures
	    config.fixture_path = "#{::Rails.root}/spec/fixtures"

	    # If you're not using ActiveRecord, or you'd prefer not to run each of your
	    # examples within a transaction, remove the following line or assign false
	    # instead of true.
	    config.use_transactional_fixtures = true

	    # If true, the base class of anonymous controllers will be inferred
	    # automatically. This will be the default behavior in future versions of
	    # rspec-rails.
	    config.infer_base_class_for_anonymous_controllers = false

	    # Run specs in random order to surface order dependencies. If you find an
	    # order dependency and want to debug it, you can fix the order by providing
	    # the seed, which is printed after each run.
	    #     --seed 1234
	    config.order = "random"
	    config.include Capybara::DSL
	  end
	end

	Spork.each_run do
	  # This code will be run each time you run your specs.

	end

Before running Spork, we can get a *baseline for the testing overhead* by timing our test suite as follows:

	$ time bundle exec rspec spec/requests/static_pages_spec.rb
	........

	Finished in 0.20196 seconds
	8 examples, 0 failures

	Randomized with seed 43027


	real	0m3.938s
	user	0m3.288s
	sys		0m0.600s

To speed this up, we can open a dedicated terminal window, navigate to the application root directory, and then start a Spork server:

	$ bundle exec spork
	Using RSpec, Rails
	Preloading Rails environment
	Loading Spork.prefork block...
	Spork is ready and listening on 8989!

In *another terminal window*, we can now run our test suite with the **--drb** (“distributed Ruby”) option and verify that the environment-loading overhead is greatly reduced:

	$ time bundle exec rspec spec/requests/static_pages_spec.rb --drb
	........

	Finished in 0.26095 seconds
	8 examples, 0 failures

	Randomized with seed 38215


	real	0m0.937s
	user	0m0.516s
	sys		0m0.076s

It’s inconvenient to have to include the **--drb** option every time we run rspec, so I recommend adding it to the **.rspec** file in the application’s root directory:

	Listing 3.38: Configuring RSpec to automatically use Spork
	--colour
	--drb

**One word of advice when using Spork**: after changing a file included in the prefork loading (such as **routes.rb**), you will have to *restart the Spork server to load the new Rails environment*. If your tests are failing when you think they should be passing, quit the Spork server with *Ctrl-C* and restart it:

	$ bundle exec spork
	Using RSpec
	Loading Spork.prefork block...
	Spork is ready and listening on 8989!
	^C
	$ bundle exec spork

#### Guard with Spork
Spork is especially useful when used with Guard, which we can arrange as follows:

	$ bundle exec guard init spork

We then need to change the **Guardfile**:

	Listing 3.39: The Guardfile updated for Spork.
	require 'active_support/inflector'

	guard 'spork', :cucumber_env => { 'RAILS_ENV' => 'test' },
	               :rspec_env    => { 'RAILS_ENV' => 'test' } do
	  watch('config/application.rb')
	  watch('config/environment.rb')
	  watch('config/environments/test.rb')
	  watch(%r{^config/initializers/.+\.rb$})
	  watch('Gemfile')
	  watch('Gemfile.lock')
	  watch('spec/spec_helper.rb') { :rspec }
	  watch('test/test_helper.rb') { :test_unit }
	  watch(%r{features/support/}) { :cucumber }
	end

	guard 'rspec', all_after_pass: false, cli: '--drb' do
	  .
	  .
	  .
	end

Note that we’ve updated the arguments to guard to include **cli: '--drb'**, which ensures that Guard uses the command-line interface (cli) to the Spork server. We’ve also added a command to watch the **features/support/** directory, which we’ll start modifying in Chapter 5.

With that configuration in place, we can start Guard and Spork at the same time with the guard command:

	$ bundle exec guard

Guard automatically starts a Spork server, dramatically reducing the overhead each time a test gets run.

A well-configured testing environment with **Guard**, **Spork**, and (optionally) *test notifications* makes test-driven development positively addictive.

### 3.6.4 - Tests inside Sublime Text
If you’re using *Sublime Text*, there is a powerful set of helper commands to run tests directly inside the editor. This is currently *my preferred setup*, as it works great when you only have a few tests while still scaling nicely even to very large (and therefore long-running) test suites. To get them working, follow the instructions for your platform at Sublime Text 2 Ruby Tests.

After restarting Sublime Text, the RubyTest package supplies the following commands: (Keys: 'Command' (OSX) 'Ctrl' (Linux / Windows))

- **Command-Shift-R**: run a single test (if run on an **it** block) or group of tests (if run on a **describe** block)
- **Command-Shift-E**: run the last test(s)
- **Command-Shift-T**: run all the tests in current file
- Show test panel: **Command-Shift-X** (when test panel visible hit esc to hide it)
- Check RB, ERB file syntax: **Alt-Shift-V**
- Switching between code and test (create a file if not found):
- Single View: **Command-.**
- Split View: **Command-Ctrl-.**
- Easy file creation: **Command-Shift-C**

Because test suites can become quite slow even for relatively small projects, being able to run one test (or a small group of tests) at a time can be a huge win. Even a single test requires the same Rails environment overhead, of course, which is why these commands are perfectly complemented by **Spork**: running a single test eliminates the overhead of running the entire test file, while running **Spork** eliminates the overhead of starting the test environment. Here is the sequence I recommend:

1. Start **Spork** in a terminal window.
2. Write a single test or small group of tests.
3. Run **Command-Shift-R** to verify that the test or test group is red.
4. Write the corresponding application code.
5. Run **Command-Shift-E** to run the same test/group again, verifying that it’s green.
6. Repeat steps 2–5 as necessary.
7. When reaching a natural *stopping point* (such as before a commit), run **rspec spec/** at the command line to confirm that the entire test suite is still green.