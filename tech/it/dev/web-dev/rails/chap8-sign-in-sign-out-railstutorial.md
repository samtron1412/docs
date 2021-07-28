[TOC]

Now that new users can sign up for our site (Chapter 7), it’s time to give registered users the ability to sign in and sign out. This will allow us to add customizations based on signin status and based on the identity of the current user. For example, in this chapter we’ll update the site header with *signin/signout links and a profile link*. In Chapter 10, we’ll use the *identity of a signed-in user to create microposts associated with that user*, and in Chapter 11 we’ll allow the current user to follow other users of the application (thereby receiving a feed of their microposts).

Having users sign in will also allow us to implement a **security model**, restricting access to particular pages based on the identity of the signed-in user. For instance, as we’ll see in Chapter 9, only signed-in users will be able to access the page used to edit user information. The signin system will also make possible special privileges for administrative users, such as the ability (also introduced in Chapter 9) to delete users from the database.

After implementing the core authentication machinery, we’ll take a short detour to investigate **Cucumber**, a popular system for behavior-driven development (Section 8.3). In particular, we’ll re-implement a couple of the RSpec integration tests in Cucumber to see how the two methods compare.

As in previous chapters, we’ll do our work on a topic branch and merge in the changes at the end:

	$ git checkout -b sign-in-out

# 8.1 - Sessions and signin failure
A [session](http://en.wikipedia.org/wiki/Session_(computer_science)) is **a semi-permanent connection between two computers**, such as a client computer running a web browser and a server running Rails. We’ll be using sessions to implement the common pattern of “signing in”, and in this context there are several different models for session behavior common on the web: **“forgetting”** the session on browser close, using an optional **“remember me”** checkbox for persistent sessions, and automatically remembering sessions until the user explicitly signs out. We’ll opt for the final of these options: when users sign in, we will remember their signin status “forever”, clearing the session only when the user explicitly signs out.

Another common model is to **expire the session after a certain amount of time**. This is especially appropriate on sites containing sensitive information, such as banking and financial trading accounts.

It’s convenient to model sessions as a RESTful resource: we’ll have a *signin page for new sessions*, *signing in will create a session*, and *signing out will destroy it*. Unlike the Users resource, which uses a database back-end (via the User model) to persist data, the Sessions resource will use a [cookie](http://en.wikipedia.org/wiki/HTTP_cookie), which is a *small piece of text placed on the user’s browser*. Much of the work involved in signin comes from building this cookie-based authentication machinery. In this section and the next, we’ll prepare for this work by constructing a Sessions controller, a signin form, and the relevant controller actions. We’ll then complete user signin in Section 8.2 by adding the necessary cookie-manipulation code.

## 8.1.1 - Sessions controller
The elements of signing in and out correspond to particular REST actions of the Sessions controller: *the signin form is handled by the new action* (covered in this section), *actually signing in is handled by sending a POST request to the create action* (Section 8.1 and Section 8.2), and *signing out is handled by sending a DELETE request to the destroy action* (Section 8.2.6).

To get started, we’ll generate a Sessions controller and an integration test for the authentication machinery:

	$ rails generate controller Sessions --no-test-framework
	$ rails generate integration_test authentication_pages

Following the model from Section 7.2 for the signup page, we’ll create a signin form for creating new sessions, as mocked up in Figure 8.1.

<figure>
  <figcaption style="text-align:center;">Figure 8.1: A mockup of the signin form.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/signin_mockup_bootstrap.png" alt="signin mockup" title="signin mockup">
</figure>

The signin page will live at the URL given by signin_path (defined momentarily), and as usual we’ll start with a minimalist test, as shown in Listing 8.1. (Compare to the analogous code for the signup page in Listing 7.6.)

	Listing 8.1: Tests for the new session action and view.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do

	  subject { page }

	  describe "signin page" do
	    before { visit signin_path }

	    it { should have_content('Sign in') }
	    it { should have_title('Sign in') }
	  end
	end

The tests initially fail, as required:

	$ bundle exec rspec spec/

To get the tests in Listing 8.1 to pass, we first need to define routes for the Sessions resource, together with a custom named route for the signin page (which we’ll map to the Session controller’s new action). As with the Users resource, we can use the resources method to define the standard RESTful routes:

	resources :sessions, only: [:new, :create, :destroy]

Since we have no need to show or edit sessions, we’ve restricted the actions to new, create, and destroy using the **:only** option accepted by resources. The full result, including named routes for signin and signout, appears in Listing 8.2.

	Listing 8.2: Adding a resource to get the standard RESTful actions for sessions.
	config/routes.rb
	 SampleApp::Application.routes.draw do
	  resources :users
	  resources :sessions, only: [:new, :create, :destroy]
	  root  'static_pages#home'
	  match '/signup',  to: 'users#new',            via: 'get'
	  match '/signin',  to: 'sessions#new',         via: 'get'
	  match '/signout', to: 'sessions#destroy',     via: 'delete'
	  .
	  .
	  .
	end

The resources defined in Listing 8.2 provide URLs and actions similar to those for users (Table 7.1), as shown in Table 8.1. Note that the routes for signin and signout are custom, but the route for creating a session is simply the default (i.e., *[resource name]_path*).

HTTP request |	URL |	Named route |	Action |	Purpose
-|-|-|-|-
GET |	/signin |	signin_path |	new |	page for a new session (signin)
POST |	/sessions |	sessions_path |	create |	create a new session
DELETE |	/signout |	signout_path |	destroy |	delete a session (sign out)

By the way, if you ever want a complete list of the routes for your application, you can use the rake routes command to have Rails generate it for you:

	$ rake routes

The next step to get the tests in Listing 8.1 to pass is to add a new action to the Sessions controller, as shown in Listing 8.3 (which also defines the create and destroy actions for future reference).

	Listing 8.3: The initial Sessions controller.
	app/controllers/sessions_controller.rb
	 class SessionsController < ApplicationController

	  def new
	  end

	  def create
	  end

	  def destroy
	  end
	end

The final step is to define the initial version of the signin page. Note that, since it is the page for a new session, the signin page lives in the file app/views/sessions/new.html.erb, which we have to create. The contents, which for now only define the page title and top-level heading, appear as in Listing 8.4.

	Listing 8.4: The initial signin view.
	app/views/sessions/new.html.erb
	 <% provide(:title, "Sign in") %>
	<h1>Sign in</h1>

With that, the tests in Listing 8.1 should be passing, and we’re ready to make the actual signin form.

	$ bundle exec rspec spec/

## 8.1.2 - Signin tests
<figure>
  <figcaption style="text-align:center;">Figure 8.2: A mockup of signin failure.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/signin_failure_mockup_bootstrap.png" alt="signin mockup" title="signin mockup">
</figure>

when the signin information is invalid we want to re-render the signin page and display an error message. We’ll render the error as a flash message, which we can test for as follows:

	it { should have_selector('div.alert.alert-error') }

This uses the Capybara method `have_selector` seen before in the solutions to two exercises, Listing 5.38 and Listing 7.32. The **have_selector** method checks for a particular selector element. which checks for a **div** tag. In particular, recalling that the dot means “class” in CSS (Section 5.1.2), you might be able to guess that this tests for a div tag with the classes *"alert" and "alert-error"*.

	Listing 8.5: The tests for signin failure.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "signin" do
	    before { visit signin_path }

	    describe "with invalid information" do
	      before { click_button "Sign in" }

	      it { should have_title('Sign in') }
	      it { should have_selector('div.alert.alert-error') }
	    end
	  end
	end


<figure>
  <figcaption style="text-align:center;">Figure 8.3: A mockup of the user profile after a successful signin.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/signin_success_mockup_bootstrap.png" alt="signin mockup" title="signin mockup">
</figure>

The test code for signin success appears in Listing 8.6.

	Listing 8.6: Test for signin success.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "signin" do
	    before { visit signin_path }
	    .
	    .
	    .
	    describe "with valid information" do
	      let(:user) { FactoryGirl.create(:user) }
	      before do
	        fill_in "Email",    with: user.email.upcase
	        fill_in "Password", with: user.password
	        click_button "Sign in"
	      end

	      it { should have_title(user.name) }
	      it { should have_link('Profile',     href: user_path(user)) }
	      it { should have_link('Sign out',    href: signout_path) }
	      it { should_not have_link('Sign in', href: signin_path) }
	    end
	  end
	end

## 8.1.3 - Signin form
The main difference between this and the signup form is that we have no Session model, and hence no analogue for the **@user** variable. This means that, in constructing the new session form, we have to give **form_for** slightly more information;

	Listing 8.7: Code for the signin form.
	app/views/sessions/new.html.erb
	 <% provide(:title, "Sign in") %>
	<h1>Sign in</h1>

	<div class="row">
	  <div class="span6 offset3">
	    <%= form_for(:session, url: sessions_path) do |f| %>

	      <%= f.label :email %>
	      <%= f.text_field :email %>

	      <%= f.label :password %>
	      <%= f.password_field :password %>

	      <%= f.submit "Sign in", class: "btn btn-large btn-primary" %>
	    <% end %>

	    <p>New user? <%= link_to "Sign up now!", signup_path %></p>
	  </div>
	</div>

## 8.1.4 - Reviewing form submission
	Listing 8.9: A preliminary version of the Sessions create action.
	app/controllers/sessions_controller.rb
	class SessionsController < ApplicationController
	.
	.
	def create
	  user = User.find_by(email: params[:session][:email].downcase)
	  if user && user.authenticate(params[:session][:password])
	    # Sign the user in and redirect to the user's show page.
	  else
	    # Create an error message and re-render the signin form.
	  end
	end
	.
	.
	end

## 8.1.5 - Rendering with a flash message
Recall from Section 7.3.3 that we displayed signup errors using the User model error messages. These errors are associated with a particular Active Record object, but this strategy won’t work here because *the session isn’t an Active Record model*. Instead, we’ll put a message in the **flash** to be displayed upon failed signin. A first, slightly incorrect, attempt appears in Listing 8.10.

	Listing 8.10: An (unsuccessful) attempt at handling failed signin.
	app/controllers/sessions_controller.rb
	 class SessionsController < ApplicationController

	  def new
	  end

	  def create
	    user = User.find_by(email: params[:session][:email].downcase)
	    if user && user.authenticate(params[:session][:password])
	      # Sign the user in and redirect to the user's show page.
	    else
	      flash[:error] = 'Invalid email/password combination' # Not quite right!
	      render 'new'
	    end
	  end

	  def destroy
	  end
	end

Because of the flash message display in the site layout (Listing 7.27), the **flash[:error]** message automatically gets displayed; because of the Bootstrap CSS, it automatically gets nice styling.

Unfortunately, as noted in the text and in the comment in Listing 8.10, this code isn’t quite right. The page looks fine, though, so what’s the problem? The issue is that the *contents of the flash persist for one request*, but—unlike a redirect, which we used in Listing 7.28—*re-rendering a template with render doesn’t count as a request*. The result is that the flash message persists one request longer than we want. For example, if we submit invalid information, the flash is set and gets displayed on the signin page (Figure 8.6); if we then click on another page, such as the Home page, that’s the first request since the form submission, and the flash gets displayed again

add test

	describe "with invalid information" do
    before { click_button "Sign in" }
    it { should have_title('Sign in') }
    it { should have_selector('div.alert.alert-error') }
    describe "after visiting another page" do
      before { click_link "Home" }
      it { should_not have_selector('div.alert.alert-error') }
    end
	end

To get the failing test to pass, instead of flash we use **flash.now**, which is specifically designed for displaying flash messages on rendered pages; unlike the contents of flash, its contents disappear as soon as there is an additional request.

# 8.2 - Signin success
Filling in the area now occupied by the signin comment (Listing 8.12) is simple: upon successful signin, we sign the user in using the `sign_in` function, and then redirect to the profile page (Listing 8.13). We see now why this is a cheat: alas, `sign_in` doesn’t currently exist. *Writing it will occupy the rest of this section*.

	Listing 8.13: The completed Sessions controller create action (not yet working).
	app/controllers/sessions_controller.rb
	 class SessionsController < ApplicationController
	  .
	  .
	  .
	  def create
	    user = User.find_by(email: params[:session][:email].downcase)
	    if user && user.authenticate(params[:session][:password])
	      sign_in user
	      redirect_to user
	    else
	      flash.now[:error] = 'Invalid email/password combination'
	      render 'new'
	    end
	  end
	  .
	  .
	  .
	end

## 8.2.1 - Remember me
We’re now in a position to start implementing our signin model, namely, remembering user signin status “forever” and ending the session only when the user explicitly signs out. The signin functions themselves will end up crossing the traditional Model-View-Controller lines; in particular, several signin functions will need to be available in both controllers and views. You may recall from Section 4.2.5 that Ruby provides a **module** facility for packaging functions together and including them in multiple places, and that’s the plan for the authentication functions. We could make an entirely new module for authentication, but the Sessions controller already comes equipped with a module, namely, **SessionsHelper**. Moreover, such helpers are automatically included in Rails views, so all we need to do to use the Sessions helper functions in controllers is to include the module into the Application controller (Listing 8.14).

	Listing 8.14: Including the Sessions helper module into the Application controller.
	app/controllers/application_controller.rb
	 class ApplicationController < ActionController::Base
	  protect_from_forgery with: :exception
	  include SessionsHelper
	end

By default, all the *helpers are available in the views but not in the controllers*. We need the methods from the Sessions helper in both places, so we have to include it explicitly.

Because HTTP is a [stateless protocol](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#HTTP_session_state), web applications requiring user signin must implement a way to track each user’s progress from page to page. One technique for maintaining the user signin status is to use a traditional Rails session (via the special **session** function) to store a remember token equal to the user’s id:

	session[:remember_token] = user.id

This **session** object makes the user id available from page to page by *storing it in a cookie that expires upon browser close*. On each page, the application could simply call

	User.find(session[:remember_token])

to retrieve the user. Because of the way Rails handles sessions, this process is secure; if a malicious user tries to spoof the user id, Rails will detect a mismatch based on a **special session id generated for each session**.

For our application’s design choice, which involves *persistent sessions*—that is, signin status that lasts even after browser close—we need to use a permanent identifier for the signed-in user. To accomplish this, we’ll **generate a unique, secure remember token for each user and store it as a permanent cookie** rather than one that expires on browser close.

The remember token needs to be associated with a user and stored for future use, so **we’ll add it as an attribute to the User model**.

<figure>
  <figcaption style="text-align:center;">Figure 8.8: The User model with an added remember_token attribute.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/user_model_remember_token_31.png" alt="user model" title="user model">
</figure>

We’ll start with a small addition to the User model specs (Listing 8.15).

	Listing 8.15: A first test for the remember token.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do
	  .
	  .
	  .
	  it { should respond_to(:password_confirmation) }
	  it { should respond_to(:remember_token) }
	  it { should respond_to(:authenticate) }
	  .
	  .
	  .
	end

We can get this test to pass by generating a remember token at the command line:

	$ rails generate migration add_remember_token_to_users

Next we fill in the resulting migration with the code from Listing 8.16. Note that, because we expect to retrieve users by remember token, we’ve added an index (Box 6.2) to the remember_token column.

	Listing 8.16: A migration to add a remember_token to the users table.
	db/migrate/[ts]_add_remember_token_to_users.rb
	 class AddRememberTokenToUsers < ActiveRecord::Migration
	  def change
	    add_column :users, :remember_token, :string
	    add_index  :users, :remember_token
	  end
	end

Next we update the development and test databases as usual:

	$ bundle exec rake db:migrate
	$ bundle exec rake test:prepare

At this point the User model specs should be passing:

	$ bundle exec rspec spec/models/user_spec.rb

Now we have to decide what to use as a remember token. There are many mostly equivalent possibilities—essentially, **any large random string will do just fine**, as long as it’s unique. The `urlsafe_base64` method from the **SecureRandom** module in the *Ruby standard library* fits the bill: it returns a random string of *length 16* composed of the characters *A–Z, a–z, 0–9, “-”, and “_”* (for a total of 64 possibilities, thus “base64”). This means that the probability of two remember tokens colliding is a negligibly small 1/64^16=2^−96≈10^−29.

Our plan is to store the [base64](http://en.wikipedia.org/wiki/Base64) token on the browser, and then store its *hash digest* (the result of running it through a one-way [cryptographic hash funtion](http://en.wikipedia.org/wiki/Cryptographic_hash_function)) in the database.

We can then sign users in automatically by *retrieving the token from the cookie, calculating the hash digest, and then searching for a remember token matching the digest’s value*. The reason for storing only hashed tokens is so that, even if our entire database is compromised, the attacker still won’t be able to use the remember tokens to sign in. To make our remember token even more secure, we’ll plan to change it every time a user creates a new session, which means that any [hijacked sessions](http://en.wikipedia.org/wiki/Session_hijacking)—in which an attacker uses a stolen cookie to sign in as a particular user—will expire the next time a user signs in. (Session hijacking was widely publicized by the [Firesheep](http://codebutler.com/firesheep) application, which showed that remember tokens at many high-profile sites were visible when connected to public Wi-Fi networks. The solution is to use site-wide **SSL**, as described in Section 7.4.4.)

Although in the actual application we will immediately sign in a newly created user (thus creating a new remember token as a side-effect), we don’t want to rely on this behavior; a more robust practice is to ensure that **every user has a valid remember token right from the start**. To accomplish this, we’ll create an initial token using a callback, a technique introduced in Section 6.2.5 in the context of email uniqueness. In that section, we used a `before_save` callback; this time, we’ll use the closely related `before_create` callback to set the remember token when the user is first created.

To test the remember token, we first save the test user (thereby creating it, since it has never been saved), and then check that the user’s **remember_token** attribute isn’t blank. This gives us sufficient flexibility to change the random string if we ever need to. The result appears in Listing 8.17.

	Listing 8.17: A test for a valid (nonblank) remember token.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before do
	    @user = User.new(name: "Example User", email: "user@example.com",
	                     password: "foobar", password_confirmation: "foobar")
	  end

	  subject { @user }
	  .
	  .
	  .
	  describe "remember token" do
	    before { @user.save }
	    its(:remember_token) { should_not be_blank }
	  end
	end

introduces the its method, which is like it but applies the subsequent test to the given attribute rather than the subject of the test. In other words,

	its(:remember_token) { should_not be_blank }

is equivalent to

	it { expect(@user.remember_token).not_to be_blank }

The application code introduces several new elements to the User model (**app/models/user.rb**). First, we add a callback method to create a remember token immediately before creating a new user in the database:

	before_create :create_remember_token

This code, called a *method reference*, arranges for Rails to look for a method called `create_remember_token` and run it before saving the user. (In Listing 6.20, we passed before_save an explicit block, but the method reference technique is generally preferred.) Second, the method itself is only used internally by the User model, so there’s no need to expose it to outside users. As we saw in Section 7.3.2, the Ruby way to accomplish this is to use the **private** keyword:

	private

	  def create_remember_token
	    # Create the token.
	  end

Finally, the `create_remember_token` method needs to assign to one of the user attributes, and in this context it is necessary to use the self keyword in front of remember_token:

	def User.new_remember_token
	  SecureRandom.urlsafe_base64
	end
	def User.digest(token)
	  Digest::SHA1.hexdigest(token.to_s)
	end
	private
	  def create_remember_token
	    self.remember_token = User.digest(User.new_remember_token)
	  end

Note that we’ve hashed the remember token using [SHA1](https://en.wikipedia.org/wiki/SHA-1), a hashing algorithm much faster than the Bcrypt algorithm used to hash user passwords in Section 6.3.1, which is important because (as we will see in Section 8.2.2) for signed-in users it will be run on every page. SHA1 is less secure than Bcrypt, but in the present case it is more than sufficient because the token being hashed is already a 16-digit random string; the SHA1 hexdigest of such a string is essentially uncrackable.

The **digest** and **new_remember_token** methods are attached to the User class because they don’t need a user instance to work, and they are public methods (above the private line) because in Section 8.2.3 we will put them to use outside of the User model.

Putting this all together yields the User model shown in Listing 8.18.

	Listing 8.18: A before_create callback to create remember_token.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  before_save { self.email = email.downcase }
	  before_create :create_remember_token
	  .
	  .
	  .
	  def User.new_remember_token
	    SecureRandom.urlsafe_base64
	  end

	  def User.digest(token)
	    Digest::SHA1.hexdigest(token.to_s)
	  end

	  private

	    def create_remember_token
	      self.remember_token = User.digest(User.new_remember_token)
	    end
	end

By the way, the extra level of indentation on **create_remember_token** is there to make it visually apparent which methods are defined after **private**. (Experience shows that this is a wise practice.)

Since the hashed **SecureRandom.urlsafe_base64** string is definitely not blank, the tests for the User model should now be passing:

	$ bundle exec rspec spec/models/user_spec.rb

## 8.2.2 - 	A working sign_in method
Now we’re ready to write the first signin element, the `sign_in` function itself. As noted above, our desired authentication method is to place a (newly created) remember token as a cookie on the user’s browser, and then use the token to find the user record in the database as the user moves from page to page (implemented in Section 8.2.3). The result appears in Listing 8.19, and introduces the **current_user** method, which we’ll implement in Section 8.2.3.

	Listing 8.19: The complete (but not-yet-working) sign_in function.
	app/helpers/sessions_helper.rb
	 module SessionsHelper

	  def sign_in(user)
	    remember_token = User.new_remember_token
	    cookies.permanent[:remember_token] = remember_token
	    user.update_attribute(:remember_token, User.digest(remember_token))
	    self.current_user = user
	  end
	end

Here we follow the desired steps: *first*, create a new token; *second*, place the raw token in the browser cookies; *third*, save the hashed token to the database; *fourth*, set the current user equal to the given user (Section 8.2.3). As we’ll see in Section 8.2.3, setting the current user to user isn’t currently necessary because of the immediate redirect in the create action (Listing 8.13), but it’s a good idea in case we ever want to use **sign_in** without a redirect.

In Listing 8.19, note the use of **update_attribute** to save the token. As mentioned briefly in Section 6.1.5), this method allows us to update a single attribute while *bypassing the validations*—necessary in this case since we don’t have the user’s password or confirmation.

Listing 8.19 also introduces the **cookies** utility supplied by Rails, which allows us to manipulate browser cookies as if they were hashes. Each element in the cookie is itself a hash of two elements, a **value** and an optional **expires** date.

	cookies[:remember_token] = { value:   remember_token,
	                             expires: 20.years.from_now.utc }

This pattern of setting a cookie that expires 20 years in the future became so common that Rails added a special permanent method to implement it, so that we can simply write

	cookies.permanent[:remember_token] = remember_token

Under the hood, using permanent causes Rails to set the expiration to 20.years.from_now automatically.

After the cookie is set, on subsequent page views we can retrieve the user with code like

	User.find_by(remember_token: remember_token)

(As we’ll see in Listing 8.22, we’ll actually have to hash the remember token first.) Of course, cookies isn’t really a hash, since assigning to cookies actually saves a piece of text on the browser.

## 8.2.3 - Current user
	self.current_user = user

As noted just after Listing 8.19, this code will never actually be used in the present application due to the immediate redirect in Listing 8.13, but it would be dangerous for the **sign_in** method to rely on this.

The purpose of **current_user**, *accessible in both controllers and views*, is to allow constructions such as

	<%= current_user.name %>

and

	redirect_to current_user

The use of **self** in the assignment is necessary for the same essential reason noted in the discussion leading up to Listing 8.18: without self, Ruby would simply create a local variable called current_user.

To start writing the code for current_user, note that the line

	self.current_user = user

is an assignment, which **we must define**. Ruby has a special syntax for defining such an assignment function, shown in Listing 8.20.

	Listing 8.20: Defining assignment to current_user.
	app/helpers/sessions_helper.rb
	 module SessionsHelper

	  def sign_in(user)
	    .
	    .
	    .
	  end

	  def current_user=(user)
	    @current_user = user
	  end
	end

This might look confusing—most languages don’t let you use the equals sign in a method definition—but it simply defines a method `current_user=` expressly designed to handle assignment to current_user. In other words, the code

	self.current_user = ...

is automatically converted to

	current_user=(...)

thereby invoking the `current_user=` method. Its one argument is the right-hand side of the assignment, in this case the user to be signed in. The one-line method body just sets an instance variable **@current_user**, effectively storing the user for later use.

In ordinary Ruby, we could define a second method, `current_user`, designed to return the value of **@current_user**, as shown in Listing 8.21.

	Listing 8.21: A tempting but useless definition for current_user.
	module SessionsHelper

	  def sign_in(user)
	    .
	    .
	    .
	  end

	  def current_user=(user)
	    @current_user = user
	  end

	  def current_user
	    @current_user     # Useless! Don't use this line.
	  end
	end

If we did this, we would effectively replicate the functionality of `attr_accessor`, which we saw in Section 4.4.5. The problem is that it utterly fails to solve our problem: with the code in Listing 8.21, the user’s signin status would be forgotten: as soon as the user went to another page — *poof*!—the session would end and the user would be automatically signed out. This is due to the **stateless nature of HTTP interactions** (Section 8.2.1)—when the user makes a second request, all the variables get set to their defaults, which for instance variables like `@current_user` is **nil**. Hence, when a user accesses another page, even on the same application, Rails has set **@current_user** to **nil**, and the code in Listing 8.21 won’t do what you want it to do.

To avoid this problem, we can *find the user corresponding to the remember token created by the code in Listing 8.19*, as shown in Listing 8.22. Note that, because the remember token in the database is hashed, we first need to hash the token from the cookie before using it to find the user in the database. We accomplish this with the **User.digest** method defined in Listing 8.18.

	Listing 8.22: Finding the current user using the remember_token.
	app/helpers/sessions_helper.rb
	 module SessionsHelper
	  .
	  .
	  .
	  def current_user=(user)
	    @current_user = user
	  end

	  def current_user
	    remember_token = User.digest(cookies[:remember_token])
	    @current_user ||= User.find_by(remember_token: remember_token)
	  end
	end

Listing 8.22 uses the common but initially obscure `||=` (“or equals”) assignment operator (Box 8.2). Its effect is to set the `@current_user` instance variable to the user corresponding to the remember token, but only if `@current_user` is undefined. In other words, the construction

	@current_user ||= User.find_by(remember_token: remember_token)

calls the `find_by` method the first time `current_user` is called, but on subsequent invocations returns `@current_user` without hitting the database. This is only useful if `current_user` is used more than once for a single user request; in any case, **find_by** will be called at least once every time a user visits a page on the site.

## 8.2.4 - Changing the layout links
we’ll change the layout links based on signin status. In particular, as seen in the Figure 8.3 mockup, we’ll arrange for the links to change when users sign in or sign out, and we’ll also add links for listing all users and user settings (to be completed in Chapter 9) and one for the current user’s profile page.

The way to change the links in the site layout involves using an **if-else** branching structure inside of Embedded Ruby:

	<% if signed_in? %>
	  # Links for signed-in users
	<% else %>
	  # Links for non-signed-in-users
	<% end %>

This kind of code requires the existence of a **signed_in?** boolean, which we’ll now define.

A user is signed in if there is a current user in the session, i.e., if `current_user` is **non-nil**. This requires the use of the **“not” operator**, written using an exclamation point `!` and usually read as **“bang”**. In the present context, a user is signed in if current_user is not nil, as shown in Listing 8.23.

	Listing 8.23: The signed_in? helper method.
	app/helpers/sessions_helper.rb
	 module SessionsHelper

	  def sign_in(user)
	    remember_token = User.new_remember_token
	    cookies.permanent[:remember_token] = remember_token
	    user.update_attribute(:remember_token, User.digest(remember_token))
	    self.current_user = user
	  end

	  def signed_in?
	    !current_user.nil?
	  end
	  .
	  .
	  .
	end

With the **signed_in?** method in hand, we’re ready to finish the layout links. There are four new links, two of which are stubbed out (to be completed in Chapter 9):

	<%= link_to "Users", '#' %>
	<%= link_to "Settings", '#' %>

The signout link, meanwhile, uses the signout path defined in Listing 8.2:

	<%= link_to "Sign out", signout_path, method: "delete" %>

(Notice that the signout link passes a hash argument indicating that it should submit with an HTTP DELETE request.9) Finally, we’ll add a profile link as follows:

	<%= link_to "Profile", current_user %>

Here we could write

	<%= link_to "Profile", user_path(current_user) %>

but Rails allows us to link directly to the user, in this context automatically converting **current_user into user_path(current_user)**.

In the process of putting the new links into the layout, we’ll take advantage of Bootstrap’s ability to make dropdown menus, which you can read more about on the [Bootstrap components page](http://getbootstrap.com/2.3.2/components.html). The full result appears in Listing 8.24. Note in particular the CSS *ids* and *classes* related to the Bootstrap dropdown menu.

	Listing 8.24: Changing the layout links for signed-in users.
	app/views/layouts/_header.html.erb
	 <header class="navbar navbar-fixed-top navbar-inverse">
	  <div class="navbar-inner">
	    <div class="container">
	      <%= link_to "sample app", root_path, id: "logo" %>
	      <nav>
	        <ul class="nav pull-right">
	          <li><%= link_to "Home", root_path %></li>
	          <li><%= link_to "Help", help_path %></li>
	          <% if signed_in? %>
	            <li><%= link_to "Users", '#' %></li>
	            <li id="fat-menu" class="dropdown">
	              <a href="#" class="dropdown-toggle" data-toggle="dropdown">
	                Account <b class="caret"></b>
	              </a>
	              <ul class="dropdown-menu">
	                <li><%= link_to "Profile", current_user %></li>
	                <li><%= link_to "Settings", '#' %></li>
	                <li class="divider"></li>
	                <li>
	                  <%= link_to "Sign out", signout_path, method: "delete" %>
	                </li>
	              </ul>
	            </li>
	          <% else %>
	            <li><%= link_to "Sign in", signin_path %></li>
	          <% end %>
	        </ul>
	      </nav>
	    </div>
	  </div>
	</header>

The dropdown menu requires the use of Bootstrap’s JavaScript library, which we can include using the Rails asset pipeline by editing the application JavaScript file, as shown in Listing 8.25.

	Listing 8.25: Adding the Bootstrap JavaScript library to application.js.
	app/assets/javascripts/application.js
	 //= require jquery
	//= require jquery_ujs
	//= require bootstrap
	//= require turbolinks
	//= require_tree .

This uses the Sprockets library to include the Bootstrap JavaScript, which in turn is available thanks to the bootstrap-sass gem from Section 5.1.2.

With the code in Listing 8.24, all the tests should be passing:

	$ bundle exec rspec spec/

A signed-in user now sees the new links and dropdown menu defined by Listing 8.24, as shown in Figure 8.9.

<figure>
  <figcaption style="text-align:center;">Figure 8.9: A signed-in user with new links and a dropdown menu.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/profile_with_signout_link_bootstrap.png" alt="profile" title="profile">
</figure>

At this point, you should verify that you can sign in, close the browser, and then still be signed in when you visit the sample application. If you want, you can even inspect the browser cookies to see the result directly.

## 8.2.5 - Signin after signup
	Listing 8.26: Testing that newly signed-up users are also signed in.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do
	    .
	    .
	    .
	    describe "with valid information" do
	      .
	      .
	      .
	      describe "after saving the user" do
	        before { click_button submit }
	        let(:user) { User.find_by(email: 'user@example.com') }

	        it { should have_link('Sign out') }
	        it { should have_title(user.name) }
	        it { should have_selector('div.alert.alert-success', text: 'Welcome') }
	      end
	    end
	  end
	end

Here we’ve tested the appearance of the signout link to verify that the user was successfully signed in after signing up.

With the `sign_in` method from Section 8.2, getting this test to pass by actually signing in the user is easy: just add **sign_in @user** right after saving the user to the database (Listing 8.27).

	Listing 8.27: Signing in the user upon signup.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def create
	    @user = User.new(user_params)
	    if @user.save
	      sign_in @user
	      flash[:success] = "Welcome to the Sample App!"
	      redirect_to @user
	    else
	      render 'new'
	    end
	  end
	  .
	  .
	  .
	end

## 8.2.6 - Signing out
So far, the Sessions controller actions have followed the RESTful convention of using **new** for a signin page and **create** to complete the signin. We’ll continue this theme by using a **destroy** action to delete sessions, i.e., to sign out. To test this, we’ll click on the “Sign out” link and then look for the reappearance of the signin link (Listing 8.28).

	Listing 8.28: A test for signing out a user.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "signin" do
	    .
	    .
	    .
	    describe "with valid information" do
	      .
	      .
	      .
	      describe "followed by signout" do
	        before { click_link "Sign out" }
	        it { should have_link('Sign in') }
	      end
	    end
	  end
	end

As with user signin, which relied on the `sign_in` function, user signout just defers to a `sign_out` function (Listing 8.29).

	Listing 8.29: Destroying a session (user signout).
	app/controllers/sessions_controller.rb
	 class SessionsController < ApplicationController
	  .
	  .
	  .
	  def destroy
	    sign_out
	    redirect_to root_url
	  end
	end

As with the other authentication elements, we’ll put `sign_out` in the Sessions helper module. Listing 8.30 shows the steps: we first change the user’s remember token in the database (in case the cookie has been stolen, as it could still be used to authorize a user), and then we use the delete method on cookies to remove the remember token from the session; as an optional final step, we set the current user to nil. (As with the assignment in the `sign_in` method (Listing 8.19), setting the current user to **nil** isn’t currently necessary because of the immediate redirect in the destroy action, but it’s a good idea in case we ever want to use `sign_out` without a redirect.)

	Listing 8.30: The sign_out method in the Sessions helper module.
	app/helpers/sessions_helper.rb
	 module SessionsHelper

	  def sign_in(user)
	    remember_token = User.new_remember_token
	    cookies.permanent[:remember_token] = remember_token
	    user.update_attribute(:remember_token, User.digest(remember_token))
	    self.current_user = user
	  end
	  .
	  .
	  .
	  def sign_out
	    current_user.update_attribute(:remember_token,
	                                  User.digest(User.new_remember_token))
	    cookies.delete(:remember_token)
	    self.current_user = nil
	  end
	end

This completes the signup/signin/signout triumvirate, and the test suite should pass:

	$ bundle exec rspec spec/

# 8.3 - Introduction to cucumber
Having finished the foundation of the sample application’s authentication system, we’re going to take this opportunity to show how to write signin tests using Cucumber, a popular tool for behavior-driven development that enjoys significant popularity in the Ruby community. Cucumber allows the definition of **plain-text** stories describing application behavior.

## 8.3.1 - Installation and setup
To install Cucumber, first add the **cucumber-rails** gem and a utility gem called **database_cleaner** to the **:test** group in the **Gemfile** (Listing 8.31).

	Listing 8.31: Adding the cucumber-rails gem to the Gemfile.
	.
	.
	.
	group :test do
	  .
	  .
	  .
	  gem 'cucumber-rails', '1.4.0', :require => false
	  gem 'database_cleaner', github: 'bmabey/database_cleaner'
	end
	.
	.
	.

Then install as usual:

	$ bundle install

To set up the application to use Cucumber, we next generate some necessary support files and directories:

	$ rails generate cucumber:install

This creates a **features/** directory where the files associated with Cucumber will live.

## 8.3.2 - Features and steps
Cucumber features are descriptions of expected behavior using a plain-text language called [Gherkin](https://github.com/cucumber/gherkin). Gherkin tests read much like well-written RSpec examples, but because they are plain-text they are more accessible to those more comfortable reading English than Ruby code.

Our Cucumber features will implement a subset of the signin examples in Listing 8.5 and Listing 8.6. To get started, we’ll create a file in the features/ directory called **signing_in.feature**.

Cucumber features start with a short description of the feature, as follows:

	Feature: Signing in

Then they add individual scenarios. For example, to test unsuccessful signin, we could write the following scenario:

	Scenario: Unsuccessful signin
	  Given a user visits the signin page
	  When they submit invalid signin information
	  Then they should see an error message

Similarly, to test successful signin, we could add this:

	Scenario: Successful signin
	  Given a user visits the signin page
	    And the user has an account
	  When the user submits valid signin information
	  Then they should see their profile page
	    And they should see a signout link

Collecting these together yields the Cucumber feature file shown in Listing 8.32.

	Listing 8.32: Cucumber features to test user signin.
	features/signing_in.feature
	 Feature: Signing in

	  Scenario: Unsuccessful signin
	    Given a user visits the signin page
	    When they submit invalid signin information
	    Then they should see an error message

	  Scenario: Successful signin
	    Given a user visits the signin page
	      And the user has an account
	    When the user submits valid signin information
	    Then they should see their profile page
	      And they should see a signout link

To run the features, we use the cucumber executable:

	$ bundle exec cucumber features/

Compare this to

	$ bundle exec rspec spec/

In this context, it’s worth noting that, like RSpec, Cucumber can be invoked using a Rake task:

	$ bundle exec rake cucumber

All we’ve done so far is write some plain text, so it shouldn’t be surprising that the Cucumber scenarios aren’t yet passing. To get the test suite to green, we need to add a step file that maps the plain-text lines to Ruby code. The step file goes in the `features/step_definitions` directory; we’ll call it **authentication_steps.rb**.

The **Feature** and **Scenario** lines are mainly for documentation, but each of the other lines needs some corresponding Ruby. For example, the line

	Given a user visits the signin page

in the feature file gets handled by the step definition

	Given /^a user visits the signin page$/ do
	  visit signin_path
	end

In the *feature*, Given is just a string, but in the *step file* Given is a method that takes a regular expression and a block. The regex matches the text of the line in the scenario, and the contents of the block are the Ruby code needed to implement the step. In this case, “a user visits the signin page” is implemented by

	visit signin_path

If this looks familiar, it should: it’s just Capybara, which is included by default in Cucumber step files. The next two lines should also look familiar; the scenario steps

	When they submit invalid signin information
	Then they should see an error message

in the feature file are handled by these steps:

	When /^they submit invalid signin information$/ do
	  click_button "Sign in"
	end

	Then /^they should see an error message$/ do
	  expect(page).to have_selector('div.alert.alert-error')
	end

The first step also uses Capybara, while the second uses Capybara’s page object with RSpec. Evidently, all the testing work we’ve done so far with RSpec and Capybara is also useful with Cucumber.

The rest of the steps proceed similarly. The final step definition file appears in Listing 8.33. Try adding one step at a time, running

	$ bundle exec cucumber features/

each time until the tests pass.

	Listing 8.33: The complete steps needed to get the signin features to pass.
	features/step_definitions/authentication_steps.rb
	 Given /^a user visits the signin page$/ do
	  visit signin_path
	end

	When /^they submit invalid signin information$/ do
	  click_button "Sign in"
	end

	Then /^they should see an error message$/ do
	  expect(page).to have_selector('div.alert.alert-error')
	end

	Given /^the user has an account$/ do
	  @user = User.create(name: "Example User", email: "user@example.com",
	                      password: "foobar", password_confirmation: "foobar")
	end

	When /^the user submits valid signin information$/ do
	  fill_in "Email",    with: @user.email
	  fill_in "Password", with: @user.password
	  click_button "Sign in"
	end

	Then /^they should see their profile page$/ do
	  expect(page).to have_title(@user.name)
	end

	Then /^they should see a signout link$/ do
	  expect(page).to have_link('Sign out', href: signout_path)
	end

With the code in Listing 8.33, the Cucumber tests should pass:

	$ bundle exec cucumber features/

## 8.3.3 - Counterpoint: RSpec custom matchers
I find that Cucumber is *easy to read and awkward to write*, while integration tests are (for a programmer) a little harder to read and much easier to write.

We can define such a matcher in the same utilities file where we put the full_title test helper in Section 5.3.4. The code itself looks like this:

	RSpec::Matchers.define :have_error_message do |message|
	  match do |page|
	    expect(page).to have_selector('div.alert.alert-error', text: message)
	  end
	end

We can also define helper functions for common operations:

	def valid_signin(user)
	  fill_in "Email",    with: user.email
	  fill_in "Password", with: user.password
	  click_button "Sign in"
	end

# 8.4 - Conclusion
We’ve covered a lot of ground in this chapter, transforming our promising but unformed application into a site capable of the full suite of registration and login behaviors. All that is needed to complete the authentication functionality is to restrict access to pages based on signin status and user identity.

We’ll accomplish this task en route to giving users the ability to edit their information and giving administrators the ability to remove users from the system, which are the main goals of Chapter 9.

Before moving on, merge your changes back into the master branch:

	$ git add .
	$ git commit -m "Finish sign in"
	$ git checkout master
	$ git merge sign-in-out

Then push up the remote GitHub repository and the Heroku production server:

	$ git push
	$ git push heroku
	$ heroku run rake db:migrate

If have error for nomethoderror at heroku, you should run this command after all:

	$ heroku restart

# 8.5 - Exercises
1. replace `form_for` by `form_tag` at sign in view. Because signing process do not manipulate with database (active record).
2. 