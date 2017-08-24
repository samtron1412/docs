[TOC]

We’ll use an HTML form to submit user signup information to our application in Section 7.2, which will then be used to create a new user and save its attributes to the database in Section 7.4. At the end of the signup process, it’s important to render a profile page with the newly created user’s information, so we’ll begin by making a page for showing users, which will serve as the first step toward implementing the REST architecture for users (Section 2.2.2). As usual, we’ll write tests as we develop, extending the theme of using RSpec and Capybara to write succinct and expressive integration tests.

If you’re following along with version control, make a topic branch as usual:

	$ git checkout master
	$ git checkout -b sign-up

# 7.1 - Showing users
Our eventual goal for the user profile pages is to show the user’s profile image, basic user data, and a list of microposts, as mocked up in Figure 7.2. (Figure 7.2 has our first example of lorem ipsum text, which has a [fascinating story](http://www.straightdope.com/columns/read/2290/what-does-the-filler-text-lorem-ipsum-mean) that you should definitely read about some time.)

<figure>
  <figcaption style="text-align:center;">Figure 7.2: A mockup of our best guess at the final profile page.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/profile_mockup_bootstrap.png" alt="profile mockup" title="profile mockup">
</figure>

## 7.1.1 - Debug and Rails environments
As preparation for adding dynamic pages to our sample application, now is a good time to add some debug information to our site layout (Listing 7.1). This displays some useful information about each page using the built-in **debug** method and **params** variable (which we’ll learn more about in Section 7.1.2).

	Listing 7.1: Adding some debug information to the site layout.
	app/views/layouts/application.html.erb
	 <!DOCTYPE html>
	<html>
	  .
	  .
	  .
	  <body>
	    <%= render 'layouts/header' %>
	    <div class="container">
	      <%= yield %>
	      <%= render 'layouts/footer' %>
	      <%= debug(params) if Rails.env.development? %>
	    </div>
	  </body>
	</html>

To make the debug output look nice, we’ll add some rules to the custom stylesheet created in Chapter 5, as shown in Listing 7.2.

	Listing 7.2: Adding code for a pretty debug box, including a Sass mixin.
	app/assets/stylesheets/custom.css.scss
	 @import "bootstrap";

	/* mixins, variables, etc. */

	$grayMediumLight: #eaeaea;

	@mixin box_sizing {
	  -moz-box-sizing: border-box;
	  -webkit-box-sizing: border-box;
	  box-sizing: border-box;
	}
	.
	.
	.

	/* miscellaneous */

	.debug_dump {
	  clear: both;
	  float: left;
	  width: 100%;
	  margin-top: 45px;
	  @include box_sizing;
	}

This introduces the Sass *mixin* facility, in this case called **box_sizing**. A mixin allows a group of CSS rules to be packaged up and used for multiple elements, converting

The debug output in Figure 7.3 gives potentially useful information about the page being rendered:

	---
	controller: static_pages
	action: home

This is a **YAML** representation of params, which is basically a hash, and in this case identifies the controller and action for the page.

### Rails environments
Rails comes equipped with three environments: test, development, and production.

If you ever need to run a console in a different environment (to debug a test, for example), you can pass the environment as a parameter to the console script:

	  $ rails console test
	  Loading test environment
	  >> Rails.env
	  => "test"
	  >> Rails.env.test?
	  => true

As with the console, development is the default environment for the local Rails server, but you can also run it in a different environment:

	$ rails server --environment production

If you view your app running in production, it won’t work without a production database, which we can create by running rake db:migrate in production:

	$ bundle exec rake db:migrate RAILS_ENV=production

(I find it confusing that the console, server, and migrate commands specify non-default environments in three mutually incompatible ways, which is why I bothered showing all three.)

By the way, if you have deployed your sample app to Heroku, you can see its environment using the heroku command, which provides its own (remote) console:

	  $ heroku run console
	  Ruby console for yourapp.herokuapp.com
	  >> Rails.env
	  => "production"
	  >> Rails.env.production?
	  => true
## 7.1.2 - A User resource
We can get the REST-style URL to work by adding a single line to our routes file (config/routes.rb):

	resources :users

The result appears in Listing 7.3.

	Listing 7.3: Adding a Users resource to the routes file.
	config/routes.rb
	 SampleApp::Application.routes.draw do
	  resources :users
	  root  'static_pages#home'
	  match '/signup',  to: 'users#new',            via: 'get'
	  .
	  .
	  .
	end

HTTP request |	URL |	Action |	Named route |	Purpose
-|-|-|-|-
GET |	/users	| index	| users_path	| page to list all users
GET	| /users/1	| show	| user_path(user) |	page to show user
GET	| /users/new	| new	| new_user_path	| page to make a new user (signup)
POST	| /users	| create	| users_path	| create a new user
GET	| /users/1/edit	| edit	| edit_user_path(user) |	page to edit user with id 1
PATCH	| /users/1	| update	| user_path(user)	| update user
DELETE	| /users/1	| destroy	| user_path(user)	| delete user

We’ll use the standard Rails location for showing a user, which is **app/views/users/show.html.erb**. Unlike the **new.html.erb** view, which we created with the generator in Listing 5.31, the **show.html.erb** file doesn’t currently exist, so you’ll have to create it by hand, filling it with the content shown in Listing 7.4.

	Listing 7.4: A stub view for showing user information.
	app/views/users/show.html.erb
	 <%= @user.name %>, <%= @user.email %>

In order to get the user show view to work, we need to define an **@user** variable in the corresponding **show** action in the Users controller. As you might expect, we use the **find** method on the User model (Section 6.1.4) to retrieve the user from the database, as shown in Listing 7.5.

	Listing 7.5: The Users controller with a show action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController

	  def show
	    @user = User.find(params[:id])
	  end

	  def new
	  end
	end

## 7.1.3 - Testing the user show pages (with factories)
To test the user show page, we’ll need a User model object so that the code in the **show** action (Listing 7.5) has something to find:

	describe "profile page" do
	  # Replace with code to make a user variable
	  before { visit user_path(user) }

	  it { should have_content(user.name) }
	  it { should have_title(user.name) }
	end

where we need to fill in the comment with the appropriate code. This uses the **user_path** named route (Table 7.1) to generate the path to the show page for the given user. It then tests that the page content and title both contain the user’s name.

In order to make the necessary User model object, we could use Active Record to create a user with **User.create**, but experience shows that user **factories** are a more convenient way to define user objects and insert them in the database. We’ll be using the **factories** generated by [Factory Girl](http://github.com/thoughtbot/factory_girl), a Ruby gem produced by the good people at [thoughtbot](http://thoughtbot.com/). *As with RSpec, Factory Girl defines a domain-specific language in Ruby, in this case specialized for defining Active Record objects*. The syntax is simple, *relying on Ruby blocks and custom methods to define the attributes of the desired object.* For cases such as the one in this chapter, the advantage over Active Record may not be obvious, but we’ll use more advanced features of **factories** in future chapters. For example, in Section 9.3.3 it will be important to create a sequence of users with unique email addresses, and **factories** make it easy to do this.

As with other Ruby gems, we can install Factory Girl by adding a line to the **Gemfile** used by Bundler (Listing 7.7). (Since Factory Girl is only needed in the tests, we’ve put it in the **:test** group.)

	$ bundle install

We’ll put all our Factory Girl factories in the file **spec/factories.rb,** which automatically gets loaded by RSpec. The code needed to make a User factory appears in Listing 7.8.

	Listing 7.8: A factory to simulate User model objects.
	spec/factories.rb
	 FactoryGirl.define do
	  factory :user do
	    name     "Michael Hartl"
	    email    "michael@example.com"
	    password "foobar"
	    password_confirmation "foobar"
	  end
	end

By passing the symbol **:user** to the factory command, we tell Factory Girl that the subsequent definition is for a User model object.

With the definition in Listing 7.8, we can create a User factory in the tests using the **let** command (Box 6.3) and the FactoryGirl method supplied by Factory Girl:

	let(:user) { FactoryGirl.create(:user) }

The final result appears in Listing 7.9.

	Listing 7.9: A test for the user show page.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do

	  subject { page }

	  describe "profile page" do
	    let(:user) { FactoryGirl.create(:user) }
	    before { visit user_path(user) }

	    it { should have_content(user.name) }
	    it { should have_title(user.name) }
	  end

	  describe "signup page" do
	    before { visit signup_path }

	    it { should have_content('Sign up') }
	    it { should have_title(full_title('Sign up')) }
	  end
	end

You should verify at this point that the test suite is red:

	$ bundle exec rspec spec/

We can get the tests to green with the code in Listing 7.10.

	Listing 7.10: Adding a title and heading for the user profile page.
	app/views/users/show.html.erb
	 <% provide(:title, @user.name) %>
	<h1><%= @user.name %></h1>

Running the tests again should confirm that the test in Listing 7.9 is passing:

	$ bundle exec rspec spec/

One thing you will quickly notice when running tests with Factory Girl is that they are *slow*. The reason is not Factory Girl’s fault, and in fact it is a feature, not a bug. The issue is that the bcrypt algorithm used in Section 6.3.1 to create a secure password hash is slow by design: bcrypt’s slow speed is part of what makes it so hard to attack. Unfortunately, this means that creating users can bog down the test suite; happily, there is an easy fix. The *bcrypt-ruby* library uses a cost factor to control how computationally costly it is to create the secure hash. The default value is designed for security, not for speed, which is perfect for *production* applications, but in *tests* our needs are reversed: we want fast tests, and don’t care at all about the security of the test users’ password hashes. The solution is to add a line to the test configuration file, **config/environments/test.rb**, redefining the cost factor from its secure default value to its fast minimum value, as shown in Listing 7.11. Even for a small test suite, the gains in speed from this step can be considerable, and I strongly recommend including Listing 7.11 in your test.rb configuration.

	Listing 7.11: Redefining the Bcrypt cost factor in a test environment.
	config/environments/test.rb
	 SampleApp::Application.configure do
	  .
	  .
	  .
	  # Speed up tests by lowering bcrypt's cost function.
	  ActiveModel::SecurePassword.min_cost = true
	end

## 7.1.4 - A Gravatar image and a sidebar
Gravatar is a free service that allows users to upload images and associate them with email addresses they control. Gravatars are a convenient way to include user profile images without going through the trouble of managing image upload, cropping, and storage; all we need to do is construct the proper Gravatar image URL using the user’s email address and the corresponding Gravatar image will automatically appear.

Our plan is to define a **gravatar_for** helper function to return a Gravatar image for a given user, as shown in Listing 7.12.

	Listing 7.12: The user show view with name and Gravatar.
	app/views/users/show.html.erb
	 <% provide(:title, @user.name) %>
	<h1>
	  <%= gravatar_for @user %>
	  <%= @user.name %>
	</h1>

You can verify at this point that the test suite is failing:

	$ bundle exec rspec spec/

Because the **gravatar_for** method is undefined, the user show view is currently broken. (Catching errors of this nature is perhaps the most useful aspect of view specs. This is why having some test of the view, even a minimalist one, is so important.)

By default, methods defined in any helper file are automatically available in any view, but for convenience we’ll put the **gravatar_for** method in the file for helpers associated with the Users controller. As [noted at the Gravatar home page](http://en.gravatar.com/site/implement/hash/), Gravatar URLs are based on an MD5 hash of the user’s email address. In Ruby, the MD5 hashing algorithm is implemented using the **hexdigest** method, which is part of the **Digest** library:

	>> email = "MHARTL@example.COM".
	>> Digest::MD5::hexdigest(email.downcase)
	=> "1fda4469bcbec3badf5418269ffc5968"

Since email addresses are case-insensitive (Section 6.2.4) but MD5 hashes are not, we’ve used the **downcase** method to ensure that the argument to hexdigest is all lower-case. The resulting **gravatar_for** helper appears in Listing 7.13.

	Listing 7.13: Defining a gravatar_for helper method.
	app/helpers/users_helper.rb
	 module UsersHelper

	  # Returns the Gravatar (http://gravatar.com/) for the given user.
	  def gravatar_for(user)
	    gravatar_id = Digest::MD5::hexdigest(user.email.downcase)
	    gravatar_url = "https://secure.gravatar.com/avatar/#{gravatar_id}"
	    image_tag(gravatar_url, alt: user.name, class: "gravatar")
	  end
	end

The code in Listing 7.13 returns an image tag for the Gravatar with a "gravatar" class and alt text equal to the user’s name (which is especially convenient for sight-impaired users using a screen reader). You can confirm that the test suite is now passing:

	$ bundle exec rspec spec/

The last element needed to complete the mockup from Figure 7.1 is the *initial version of the user sidebar*. We’ll implement it using the **aside** tag, which is used for content (such as sidebars) that complements the rest of the page but can also stand alone. We include **row** and **span4** classes, which are both part of Bootstrap. The code for the modified user show page appears in Listing 7.14.

	Listing 7.14: Adding a sidebar to the user show view.
	app/views/users/show.html.erb
	 <% provide(:title, @user.name) %>
	<div class="row">
	  <aside class="span4">
	    <section>
	      <h1>
	        <%= gravatar_for @user %>
	        <%= @user.name %>
	      </h1>
	    </section>
	  </aside>
	</div>

With the HTML elements and CSS classes in place, we can style the profile page (including the sidebar and the Gravatar) with the SCSS shown in Listing 7.15. (Note the nesting of the table CSS rules, which works only because of the Sass engine used by the asset pipeline.) The resulting page is shown in Figure 7.9.

	Listing 7.15: SCSS for styling the user show page, including the sidebar.
	app/assets/stylesheets/custom.css.scss
	 .
	.
	.

	/* sidebar */

	aside {
	  section {
	    padding: 10px 0;
	    border-top: 1px solid $grayLighter;
	    &:first-child {
	      border: 0;
	      padding-top: 0;
	    }
	    span {
	      display: block;
	      margin-bottom: 3px;
	      line-height: 1;
	    }
	    h1 {
	      font-size: 1.4em;
	      text-align: left;
	      letter-spacing: -1px;
	      margin-bottom: 3px;
	      margin-top: 0px;
	    }
	  }
	}

	.gravatar {
	  float: left;
	  margin-right: 10px;
	}


# 7.2 - Singup form
Since we’re about to add the ability to create new users through the web, let’s remove the user created at the console in Section 6.3.5. The cleanest way to do this is to reset the database with the **db:reset** Rake task:

	$ bundle exec rake db:reset

After resetting the database, on some systems the test database needs to be re-prepared as well:

	$ bundle exec rake test:prepare

Finally, on some systems you might have to restart the web server (using Ctrl-C) for the changes to take effect.

## 7.2.1 - Tests for user signup
We’ve already seen how *Capybara* supports an intuitive web-navigation syntax. So far, we’ve mostly used **visit** to visit particular pages, but *Capybara* can do a lot more, including filling in the kind of fields we see in Figure 7.11 and clicking on the button. The syntax looks like this:

	visit signup_path
	fill_in "Name", with: "Example User"
	.
	.
	.
	click_button "Create my account"

Our goal now is to write tests for the right behavior given invalid and valid signup information. Because these tests are fairly advanced, we’ll build them up piece by piece. If you want to see how they work (including which file to put them in), you can skip ahead to Listing 7.16.

Our first task is to test for a failing signup form, and we can simulate the submission of invalid data by visiting the page and clicking the button using **click_button**:

	visit signup_path
	click_button "Create my account"

This is equivalent to visiting the signup page and submitting blank signup information (which is invalid). Similarly, to simulate the submission of valid data, we fill in valid information using **fill_in**:

	visit signup_path
	fill_in "Name",         with: "Example User"
	fill_in "Email",        with: "user@example.com"
	fill_in "Password",     with: "foobar"
	fill_in "Confirmation", with: "foobar"
	click_button "Create my account"

The purpose of our tests is to verify that clicking the signup button results in the correct behavior, creating a new user when the information is valid and not creating a user when it’s invalid. The way to do this is to *check the count of users*, and under the hood our tests will use the count method available on every Active Record class, including User:

	$ rails console
	>> User.count
	=> 0
	Here User.count is 0 because we reset the database at the beginning of this section.

When submitting invalid data, we expect the user count not to change; when submitting valid data, we expect it to change by 1. We can express this in RSpec by combining the **expect** method with either the **to** method or the **not_to** method. We’ll start with the invalid case since it is simpler; we visit the signup path and click the button, and we expect it not to change the user count:

	visit signup_path
	expect { click_button "Create my account" }.not_to change(User, :count)

Note that, as indicated by the curly braces, expect wraps **click_button** in a block (Section 4.3.2). This is for the benefit of the change method, which takes as arguments an object and a symbol and then calculates the result of calling that symbol as a method on the object both before and after the block. In other words, the code

	expect { click_button "Create my account" }.not_to change(User, :count)

calculates

	User.count

before and after the execution of

	click_button "Create my account"

In the present case, we want the given code not to change the count, which we express using the **not_to** method. In effect, by enclosing the button click in a block we are able to replace

	initial = User.count
	click_button "Create my account"
	final = User.count
	expect(initial).to eq final

with the single line

	expect { click_button "Create my account" }.not_to change(User, :count)

which reads like natural language and is much more compact. (Note that **eq** is an RSpec method to test equality.)

The case of valid data is similar, but instead of verifying that the user count doesn’t change, we check that clicking the button changes the count by 1:

	visit signup_path
	fill_in "Name",         with: "Example User"
	fill_in "Email",        with: "user@example.com"
	fill_in "Password",     with: "foobar"
	fill_in "Confirmation", with: "foobar"
	expect do
	  click_button "Create my account"
	end.to change(User, :count).by(1)

This uses the to method because we expect a click on the signup button with valid data to change the user count by one.

Combining the two cases with the appropriate describe blocks and pulling the common code into before blocks yields good basic tests for signing up users, as shown in Listing 7.16. Here we’ve factored out the common text for the submit button using the let method to define a submit variable.

	Listing 7.16: Good basic tests for signing up users.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do

	  subject { page }
	  .
	  .
	  .
	  describe "signup page" do
	    before { visit signup_path }

	    it { should have_content('Sign up') }
	    it { should have_title(full_title('Sign up')) }
	  end

	  describe "signup" do

	    before { visit signup_path }

	    let(:submit) { "Create my account" }

	    describe "with invalid information" do
	      it "should not create a user" do
	        expect { click_button submit }.not_to change(User, :count)
	      end
	    end

	    describe "with valid information" do
	      before do
	        fill_in "Name",         with: "Example User"
	        fill_in "Email",        with: "user@example.com"
	        fill_in "Password",     with: "foobar"
	        fill_in "Confirmation", with: "foobar"
	      end

	      it "should create a user" do
	        expect { click_button submit }.to change(User, :count).by(1)
	      end
	    end
	  end
	end

We’ll add a few more tests as needed in the sections that follow, but the basic tests in Listing 7.16 already cover an impressive amount of functionality. To get them to pass, we have to create a signup page with just the right elements, arrange for the page’s submission to be routed to the right place, and successfully create a new user in the database only if the resulting user data is valid.

Of course, at this point the tests should fail:

	$ bundle exec rspec spec/

## 7.2.2 - Using form_for
Now that we have good failing tests for user signup, we’ll start getting them to pass by making a form for signing up users. We can accomplish this in Rails with the `form_for` helper method, which takes in an Active Record object and constructs a form using the object’s attributes. The result appears in Listing 7.17. (Readers familiar with Rails 2.x should note that **form_for** uses the “percent-equals” ERb syntax for inserting content; that is, where Rails 2.x used **<% form_for ... %>**, we now use **<%= form_for ... %>** instead.)

	Listing 7.17: A form to sign up new users.
	app/views/users/new.html.erb
	 <% provide(:title, 'Sign up') %>
	<h1>Sign up</h1>

	<div class="row">
	  <div class="span6 offset3">
	    <%= form_for(@user) do |f| %>

	      <%= f.label :name %>
	      <%= f.text_field :name %>

	      <%= f.label :email %>
	      <%= f.text_field :email %>

	      <%= f.label :password %>
	      <%= f.password_field :password %>

	      <%= f.label :password_confirmation, "Confirmation" %>
	      <%= f.password_field :password_confirmation %>

	      <%= f.submit "Create my account", class: "btn btn-large btn-primary" %>
	    <% end %>
	  </div>
	</div>

Let’s break this down into pieces. The presence of the do keyword indicates that form_for takes a block with one variable, which we’ve called f for “form”:

	<%= form_for(@user) do |f| %>
	  .
	  .
	  .
	<% end %>

As is usually the case with Rails helpers, we don’t need to know any details about the implementation, but what we do need to know is what the **f** object does: when called with a method corresponding to an HTML form element—such as a text field, radio button, or password field—it returns code for that element specifically designed to set an attribute of the **@user** object. In other words,

	<%= f.label :name %>
	<%= f.text_field :name %>

creates the HTML needed to make a labeled text field element appropriate for setting the name attribute of a User model. (We’ll take a look at the HTML itself in Section 7.2.3.)

To see this in action, we need to drill down and look at the actual HTML produced by this form, but here we have a problem: the page currently breaks, because we have not set the **@user** variable—like all undefined instance variables (Section 4.4.5), **@user** is currently **nil**.

we must define an **@user** variable in the controller action corresponding to **new.html.erb**, i.e., the new action in the Users controller. The form_for helper expects **@user** to be a User object, and since we’re creating a new user we simply use **User.new**, as seen in Listing 7.18.

	Listing 7.18: Adding an @user variable to the new action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def new
	    @user = User.new
	  end
	end

At this point, the form (with the styling from Listing 7.19) appears as in Figure 7.12. Note the reuse of the **box_sizing** mixin from Listing 7.2.

	Listing 7.19: CSS for the signup form.
	app/assets/stylesheets/custom.css.scss
	 .
	.
	.

	/* forms */

	input, textarea, select, .uneditable-input {
	  border: 1px solid #bbb;
	  width: 100%;
	  margin-bottom: 15px;
	  @include box_sizing;
	}

	input {
	  height: auto !important;
	}

## 7.2.3 - The form HTML
Rails automatically includes to thwart a particular kind of attack called a **cross-site request forgery**(CSRF). See [the Stack Overflow entry on the Rails authenticity token](http://stackoverflow.com/questions/941594/understand-rails-authenticity-token) if you’re interested in the details of how this works and why it’s important.

we see that the Embedded Ruby

	<%= f.label :name %>
	<%= f.text_field :name %>

produces the HTML

	<label for="user_name">Name</label>
	<input id="user_name" name="user[name]" type="text" />

and

	<%= f.label :password %>
	<%= f.password_field :password %>

produces the HTML

	<label for="user_password">Password</label><br />
	<input id="user_password" name="user[password]" type="password" />

As we’ll see in Section 7.4, the key to creating a user is the special **name** attribute in each input:

	<input id="user_name" name="user[name]" - - - />
	.
	.
	.
	<input id="user_password" name="user[password]" - - - />

These **name** values allow Rails to construct an initialization hash (via the params variable) for creating users using the values entered by the user, as we’ll see in Section 7.3.

The second important element is the **form** tag itself. Rails creates the **form** tag using the **@user** object: because every Ruby object knows its own class (Section 4.4.1), Rails figures out that **@user** is of class **User**; moreover, since **@user** is a new user, Rails knows to construct a **form** with the post method, which is the proper verb for creating a new object (Box 3.3):

	<form action="/users" class="new_user" id="new_user" method="post">

Here the **class** and **id** attributes are largely irrelevant; what’s important is **action="/users"** and **method="post"**. Together, these constitute instructions to issue an HTTP POST request to the **/users** URL. We’ll see in the next two sections what effects this has.

# 7.3 - Signup failure
 In this section, we’ll create a signup form that accepts an invalid submission and re-renders the signup page with a list of errors.

## 7.3.1 - A working form
This listing includes a second use of the **render** method, which we first saw in the context of partials (Section 5.1.3); as you can see, **render** works in controller actions as well. Note that we’ve taken this opportunity to introduce an **if-else** branching structure, which allows us to handle the cases of failure and success separately based on the value of **@user.save**, which (as we saw in Section 6.1.3) is either true or false depending on whether the save succeeds.

	Listing 7.21: A create action that can handle signup failure (but not success).
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def create
	    @user = User.new(params[:user])    # Not the final implementation!
	    if @user.save
	      # Handle a successful save.
	    else
	      render 'new'
	    end
	  end
	end

## 7.3.2 - Strong parameter
We mentioned briefly in Section 4.4.5 the idea of **mass assignment**, which involves initializing a Ruby variable using a hash of values, as in

	@user = User.new(params[:user])    # Not the final implementation!

The comment included in Listing 7.21 and reproduced above indicates that this is not the final implementation. The reason is that initializing the entire **params** hash is extremely dangerous—it arranges to pass to **User.new** all data submitted by a user. In particular, suppose that, in addition to the current attributes, the User model included an **admin** attribute used to identify administrative users of the site. (We will implement just such an attribute in Section 9.4.1.) The way to set such an attribute to **true** is to pass the value **admin=’1’** as part of **params[:user]**, a task that is easy to accomplish using a command-line HTTP client such as **curl**. The result would be that, by passing in the entire params hash to **User.new**, we would allow any user of the site to gain administrative access by including **admin=’1’** in the web request.

Previous versions of Rails used a method called **attr_accessible** in the model layer to solve this problem, but as of Rails 4.0 the preferred technique is to use so-called **strong parameters** in the controller layer. This allows us to specify which parameters are *required* and which ones are *permitted*. In addition, passing in a raw params hash as above will cause an error to be raised, so that Rails applications are now immune to **mass assignment** vulnerabilities by default.

In the present instance, we want to require the params hash to have a :user attribute, and we want to permit the name, email, password, and password confirmation attributes (but no others). We can accomplish this as follows:

	params.require(:user).permit(:name, :email, :password, :password_confirmation)

This code returns a version of the params hash with only the permitted attributes (while raising an error if the **:user** attribute is missing).

To facilitate the use of these parameters, it’s conventional to introduce an auxiliary method called **user_params** that returns an appropriate initialization hash and use it in place of **params[:user]**:

	@user = User.new(user_params)

Since **user_params** will only be used internally by the Users controller and need not be exposed to external users via the web, we’ll make it private using Ruby’s private keyword, as shown in Listing 7.22. (We’ll discuss private in more detail in Section 8.2.1.)

	Listing 7.22: Using strong parameters in the create action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def create
	    @user = User.new(user_params)
	    if @user.save
	      # Handle a successful save.
	    else
	      render 'new'
	    end
	  end

	  private

	    def user_params
	      params.require(:user).permit(:name, :email, :password,
	                                   :password_confirmation)
	    end
	end

## 7.3.3 - Signup error messages
Here the **errors.full_messages** object (which we saw briefly in Section 6.2.2) contains an array of error messages.

As in the console session above, the failed save in Listing 7.21 generates a list of error messages associated with the **@user** object. To display the messages in the browser, we’ll render an *error-messages partial* on the user new page, as shown in Listing 7.23. (Writing a test for the error messages first is a good idea and is left as an exercise; see Section 7.6.) It’s worth noting that this error messages partial is only a first attempt; the final version appears in Section 10.3.2.

	Listing 7.23: Code to display error messages on the signup form.
	app/views/users/new.html.erb
	 <% provide(:title, 'Sign up') %>
	<h1>Sign up</h1>

	<div class="row">
	  <div class="span6 offset3">
	    <%= form_for(@user) do |f| %>
	      <%= render 'shared/error_messages' %>
	      .
	      .
	      .
	    <% end %>
	  </div>
	</div>

Notice here that we render a partial called *’shared/error_messages’*; this reflects the common Rails convention of using a dedicated **shared/** directory for partials expected to be used in views across multiple controllers. (We’ll see this expectation fulfilled in Section 9.1.1.) This means that we have to create both the new **app/views/shared** directory and the **_error_messages.html.erb** partial file. The partial itself appears in Listing 7.24.

	Listing 7.24: A partial for displaying form submission error messages.
	app/views/shared/_error_messages.html.erb
	 <% if @user.errors.any? %>
	  <div id="error_explanation">
	    <div class="alert alert-error">
	      The form contains <%= pluralize(@user.errors.count, "error") %>.
	    </div>
	    <ul>
	    <% @user.errors.full_messages.each do |msg| %>
	      <li>* <%= msg %></li>
	    <% end %>
	    </ul>
	  </div>
	<% end %>

This partial introduces several new Rails and Ruby constructs, including two methods for Rails error objects. The first method is **count**, which simply returns the number of errors:

	>> user.errors.count
	=> 2

The other new method is **any?**, which (together with **empty?**) is one of a pair of complementary methods:

	>> user.errors.empty?
	=> false
	>> user.errors.any?
	=> true

The other new idea is the **pluralize** text helper. It isn’t available in the console by default, but we can include it explicitly through the **ActionView::Helpers::TextHelper** module:9

	>> include ActionView::Helpers::TextHelper
	>> pluralize(1, "error")
	=> "1 error"
	>> pluralize(5, "error")
	=> "5 errors"

We see here that pluralize takes an integer argument and then returns the number with a properly pluralized version of its second argument. Underlying this method is a powerful inflector that knows how to pluralize a large number of words, including many with irregular plurals:

	>> pluralize(2, "woman")
	=> "2 women"
	>> pluralize(3, "erratum")
	=> "3 errata"

As a result of its use of pluralize, the code

	<%= pluralize(@user.errors.count, "error") %>

returns "0 errors", "1 error", "2 errors", and so on, depending on how many errors there are, thereby avoiding ungrammatical phrases such as "1 errors" (a distressingly common mistake on teh interwebs).

Note that Listing 7.24 includes the CSS id *error_explanation* for use in styling the error messages. (Recall from Section 5.1.2 that CSS uses the pound sign `#` to style ids.) In addition, on error pages Rails automatically wraps the fields with errors in *divs* with the CSS class *field_with_errors*. These labels then allow us to style the error messages with the SCSS shown in Listing 7.25, which makes use of Sass’s **@extend** function to include the functionality of two Bootstrap classes control-group and error. As a result, on failed submission the error messages appear surrounded by red, as seen in Figure 7.17. Because the messages are generated by the model validations, they will automatically change if you ever change your mind about, say, the format of email addresses, or the minimum length of passwords.

	Listing 7.25: CSS for styling error messages.
	app/assets/stylesheets/custom.css.scss
	 .
	.
	.

	/* forms */
	.
	.
	.
	#error_explanation {
	  color: #f00;
	  ul {
	    list-style: none;
	    margin: 0 0 18px 0;
	  }
	}

	.field_with_errors {
	  @extend .control-group;
	  @extend .error;
	}

# 7.4 - Signup success
Having handled invalid form submissions, now it’s time to complete the signup form by actually saving a new user (if valid) to the database. First, we try to *save the user*; if the save succeeds, the user’s information gets *written to the database* automatically, and we then *redirect the browser to show the user’s profile* (together with a friendly greeting), as mocked up in Figure 7.19. If it fails, we simply fall back on the behavior developed in Section 7.3.

<figure>
  <figcaption style="text-align:center;">Figure 7.19: A mockup of successful signup.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/signup_success_mockup_bootstrap.png" alt="profile mockup" title="profile mockup">
</figure>

## 7.4.1 - The finish signup form
This is because the default behavior for a Rails action is to render the corresponding view, but there is not (nor should there be) a view template corresponding to the create action. Instead, we need to redirect to a different page, and it makes sense for that page to be the newly created user’s profile. Testing that the proper page gets rendered is left as an exercise (Section 7.6); the application code appears in Listing 7.26.

	Listing 7.26: The user create action with a save and a redirect.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def create
	    @user = User.new(user_params)
	    if @user.save
	      redirect_to @user
	    else
	      render 'new'
	    end
	  end

	  private

	    def user_params
	      params.require(:user).permit(:name, :email, :password,
	                                   :password_confirmation)
	    end
	end

Note that we can omit the *user_url* in the redirect, writing simply **redirect_to @user** to redirect to the user show page.

## 7.4.2 - The flash
Before submitting a valid registration in a browser, we’re going to add a bit of polish common in web applications: a message that appears on the subsequent page (in this case, welcoming our new user to the application) and then disappears upon visiting a second page or on page reload. The Rails way to accomplish this is to use a special variable called the flash, which we can treat like a hash.

We can arrange to display the contents of the flash site-wide by including it in our application layout, as in Listing 7.27. (This code is a particularly ugly combination of HTML and ERb; an exercise in Section 7.6 shows how to make it prettier.)

	Listing 7.27: Adding the contents of the flash variable to the site layout.
	app/views/layouts/application.html.erb
	 <!DOCTYPE html>
	<html>
	  .
	  .
	  .
	  <body>
	    <%= render 'layouts/header' %>
	    <div class="container">
	      <% flash.each do |key, value| %>
	        <div class="alert alert-<%= key %>"><%= value %></div>
	      <% end %>
	      <%= yield %>
	      <%= render 'layouts/footer' %>
	      <%= debug(params) if Rails.env.development? %>
	    </div>
	    .
	    .
	    .
	  </body>
	</html>

The code in Listing 7.27 arranges to insert a div tag for each element in the flash, with a CSS class indicating the type of message. For example, if flash[:success] = "Welcome to the Sample App!", then the code

	<% flash.each do |key, value| %>
	  <div class="alert alert-<%= key %>"><%= value %></div>
	<% end %>

will produce this HTML:

	<div class="alert alert-success">Welcome to the Sample App!</div>

(Note that the key **:success** is a symbol, but embedded Ruby automatically converts it to the string "success" before inserting it into the template.) The reason we iterate through all possible key/value pairs is so that we can include other kinds of flash messages. For example, in Section 8.1.5 we’ll see flash[:error] used to indicate a failed signin attempt.10

Writing a test for the right flash message is left as an exercise (Section 7.6), and we can get the test to pass by assigning flash[:success] a welcome message in the create action, as shown in Listing 7.28.

	Listing 7.28: Adding a flash message to user signup.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def create
	    @user = User.new(user_params)
	    if @user.save
	      flash[:success] = "Welcome to the Sample App!"
	      redirect_to @user
	    else
	      render 'new'

## 7.4.3 - The first signup
try

## 7.4.4 - Deploying to production with SSL
As part of this, we will add [Secure Sockets Layer](http://en.wikipedia.org/wiki/Transport_Layer_Security) (SSL) to the production application, thereby making signup secure. Since we’ll implement SSL site-wide, the sample application will also be secure during user signin (Chapter 8) and will also be immune to the **session hijacking** vulnerability (Section 8.2.1).

As preparation for the deployment, you should merge your changes into the **master** branch at this point:

	$ git add .
	$ git commit -m "Finish user signup"
	$ git checkout master
	$ git merge sign-up

To get the deployment to work, we first need to add a line forcing the use of SSL in production. The result, which involves editing the production configuration file **config/environments/production.rb**, appears in Listing 7.29.

	Listing 7.29: Configuring the application to use SSL in production.
	config/environments/production.rb
	 SampleApp::Application.configure do
	  .
	  .
	  .
	  # Force all access to the app over SSL, use Strict-Transport-Security,
	  # and use secure cookies.
	  config.force_ssl = true
	  .
	  .
	  .
	end

To get the production site working, we have to commit the change to the configuration file and push the result up to Heroku:

	$ git commit -a -m "Add SSL in production"
	$ git push heroku

Next, we need to run the migration on the production database to tell Heroku about the User data model:

	$ heroku run rake db:migrate

Finally, we need to set up SSL on the remote server. Configuring a production site to use SSL is painful and error-prone, and among other things it involves *purchasing an SSL certificate* for your domain. Luckily, for an application running on a *Heroku domain* (such as the sample application), we can piggyback on Heroku’s SSL certificate, a feature that is included automatically as part of the Heroku platform. If you want to run SSL on a custom domain, such as **example.com**, you’ll have no choice but to endure some pain, which you can read about on [Heroku’s page on SSL](http://devcenter.heroku.com/articles/ssl).

The result of all this work is a working signup form on the production server (Figure 7.22):

	$ heroku open

Note in Figure 7.22 the **https://** in place of the usual **http://**. The extra ‘s’ is an indication that SSL is working.

You should feel free to visit the signup page and create a new user at this time. If you have trouble, try running

	$ heroku logs

to debug the error using the Heroku logfile.


# 7.5 - Conclusion
Being able to *sign up users* is a major milestone for our application. Although the sample app has yet to accomplish anything useful, we have laid an essential foundation for all future development. In Chapter 8, we will complete our authentication machinery by allowing users to *sign in and out* of the application. In Chapter 9, we will allow all users to *update their account information, and will allow site administrators to delete users*, thereby completing the full suite of the Users resource REST actions from Table 7.1. Finally, we’ll add authorization methods to our actions to enforce a site security model.

# 7.6 - Exercises


