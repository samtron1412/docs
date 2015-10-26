[TOC]

In this chapter, we will complete the REST actions for the Users resource (Table 7.1) by adding **edit, update, index**, and **destroy** actions. To get started, let’s start work on an updating-users topic branch:

	$ git checkout -b updating-users

# 9.1 - Updating users
The pattern for editing user information closely parallels that for creating new users (Chapter 7). Instead of a **new** action rendering a view for new users, we have an **edit** action rendering a view to edit users; instead of create responding to a **POST** request, we have an update action responding to a **PATCH** request (Box 3.3). The biggest difference is that, while anyone can sign up, *only the current user should be able to update their information*. This means that we need to enforce access control so that only authorized users can edit and update; the authentication machinery from Chapter 8 will allow us to use a **before filter** to ensure that this is the case.

## 9.1.1 - Edit form
<figure>
  <figcaption style="text-align:center;">Figure 9.1: A mockup of the user edit page.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/edit_user_mockup_bootstrap.png" alt="edit mockup" title="edit mockup">
</figure>

The tests for the edit user form are analogous to the test for the new user form in Listing 7.31 from the Chapter 7 exercises, which added a test for the error message on invalid submission. The result appears in Listing 9.1.

	Listing 9.1: Tests for the user edit page.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do
	  .
	  .
	  .
	  describe "edit" do
	    let(:user) { FactoryGirl.create(:user) }
	    before { visit edit_user_path(user) }

	    describe "page" do
	      it { should have_content("Update your profile") }
	      it { should have_title("Edit user") }
	      it { should have_link('change', href: 'http://gravatar.com/emails') }
	    end

	    describe "with invalid information" do
	      before { click_button "Save changes" }

	      it { should have_content('error') }
	    end
	  end
	end

To write the application code, we need to fill in the edit action in the Users controller. Note from Table 7.1 that the proper URL for a user’s edit page is **/users/1/edit** (assuming the user’s id is 1). Recall that the id of the user is available in the **params[:id]** variable, which means that we can find the user with the code in Listing 9.2.

	Listing 9.2: The user edit action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def edit
	    @user = User.find(params[:id])
	  end
	  .
	  .
	  .
	end

Getting the tests to pass requires making the actual edit view, shown in Listing 9.3. Note how closely this resembles the new user view from Listing 7.17; the large overlap suggests *factoring the repeated code into a partial*, which is left as an exercise (Section 9.6).

	Listing 9.3: The user edit view.
	app/views/users/edit.html.erb
	 <% provide(:title, "Edit user") %>
	<h1>Update your profile</h1>

	<div class="row">
	  <div class="span6 offset3">
	    <%= form_for(@user) do |f| %>
	      <%= render 'shared/error_messages' %>

	      <%= f.label :name %>
	      <%= f.text_field :name %>

	      <%= f.label :email %>
	      <%= f.text_field :email %>

	      <%= f.label :password %>
	      <%= f.password_field :password %>

	      <%= f.label :password_confirmation, "Confirm Password" %>
	      <%= f.password_field :password_confirmation %>

	      <%= f.submit "Save changes", class: "btn btn-large btn-primary" %>
	    <% end %>

	    <%= gravatar_for @user %>
	    <a href="http://gravatar.com/emails">change</a>
	  </div>
	</div>

Here we have reused the shared **error_messages** partial introduced in Section 7.3.3.

With the @user instance variable from Listing 9.2, the edit page tests from Listing 9.1 should pass:

	$ bundle exec rspec spec/requests/user_pages_spec.rb -e "edit page"

Looking at the HTML source for Figure 9.2, we see a form tag as expected (Listing 9.4).

	Listing 9.4: HTML for the edit form defined in Listing 9.3 and shown in Figure 9.2.
	<form action="/users/1" class="edit_user" id="edit_user_1" method="post">
	  <input name="_method" type="hidden" value="patch" />
	  .
	  .
	  .
	</form>

Note here the hidden input field

	<input name="_method" type="hidden" value="patch" />

Since web browsers can’t natively send PATCH requests (as required by the REST conventions from Table 7.1), Rails fakes it with a POST request and a hidden input field.

There’s another subtlety to address here: the code `form_for(@user)` in Listing 9.3 is exactly the same as the code in Listing 7.17—so how does Rails know to use a *POST* request for new users and a *PATCH* for editing users? The answer is that it is possible to tell whether a user is new or already exists in the database via Active Record’s **new_record?** boolean method:

	$ rails console
	>> User.new.new_record?
	=> true
	>> User.first.new_record?
	=> false

When constructing a form using `form_for(@user)`, Rails uses *POST if @user.new_record? is true* and *PATCH if it is false*.

New test for sign in user

	Listing 9.5: Adding a test for the “Settings” link.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	    .
	    .
	    .
	    describe "with valid information" do
	      let(:user) { FactoryGirl.create(:user) }
	      before { sign_in user }

	      it { should have_title(user.name) }
	      it { should have_link('Profile',     href: user_path(user)) }
	      it { should have_link('Settings',    href: edit_user_path(user)) }
	      it { should have_link('Sign out',    href: signout_path) }
	      it { should_not have_link('Sign in', href: signin_path) }
	      .
	      .
	      .
	    end
	  end
	end

Two point need notice here:

1. add test *Settings* link
2. use **sign_in** function at **utilities.rb** support

```
Listing 9.6: A test helper to sign users in.
spec/support/utilities.rb
.
.
.
def sign_in(user, options={})
  if options[:no_capybara]
    # Sign in when not using Capybara.
    remember_token = User.new_remember_token
    cookies[:remember_token] = remember_token
    user.update_attribute(:remember_token, User.digest(remember_token))
  else
    visit signin_path
    fill_in "Email",    with: user.email
    fill_in "Password", with: user.password
    click_button "Sign in"
  end
end
```

As noted in the comment line, filling in the form doesn’t work when not using Capybara, so to cover this case we allow the user to pass the option `no_capybara: true` to override the default signin method and manipulate the cookies directly. This is necessary when using one of the HTTP request methods directly (**get, post, patch, or delete**), as we’ll see in Listing 9.45. (Note that the test cookies object isn’t a perfect simulation of the real cookies object; in particular, the **cookies.permanent** method seen in Listing 8.19 doesn’t work inside tests.) As you might suspect, the **sign_in** method will prove useful in future tests, and in fact it can already be used to eliminate some duplication.

The application code to add the URL for the *“Settings”* link is simple: we just use the named route **edit_user_path** from Table 7.1, together with the handy **current_user** helper method defined in Listing 8.22:

	<%= link_to "Settings", edit_user_path(current_user) %>

Edit file **_header.html.erb** link for Settings

## 9.1.2 - Unsuccessful edits
In this section we’ll handle unsuccessful edits and get the error messages test in Listing 9.1 to pass. The application code creates an update action that uses **update_attributes** (Section 6.1.5) to update the user based on the submitted params hash, as shown in Listing 9.8. With invalid information, the update attempt returns false, so the else branch re-renders the edit page. We’ve seen this pattern before; the structure closely parallels the first version of the **create** action (Listing 7.21).

	Listing 9.8: The initial user update action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def edit
	    @user = User.find(params[:id])
	  end

	  def update
	    @user = User.find(params[:id])
	    if @user.update_attributes(user_params)
	      # Handle a successful update.
	    else
	      render 'edit'
	    end
	  end
	  .
	  .
	  .
	end

Note the use of `user_params` in the call to **update_attributes**, which uses strong parameters to prevent *mass assignment vulnerability* (as described in Section 7.3.2).

The resulting error message (Figure 9.3) is the one needed to get the error message test to pass, as you should verify by running the test suite:

	$ bundle exec rspec spec/

## 9.1.3 - Successful edits
The tests for the **update** action are similar to those for **create**.

	Listing 9.9: Tests for the user update action.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do
	  .
	  .
	  .
	  describe "edit" do
	    let(:user) { FactoryGirl.create(:user) }
	    before do
	      sign_in user
	      visit edit_user_path(user)
	    end
	    .
	    .
	    .
	    describe "with valid information" do
	      let(:new_name)  { "New Name" }
	      let(:new_email) { "new@example.com" }
	      before do
	        fill_in "Name",             with: new_name
	        fill_in "Email",            with: new_email
	        fill_in "Password",         with: user.password
	        fill_in "Confirm Password", with: user.password
	        click_button "Save changes"
	      end

	      it { should have_title(new_name) }
	      it { should have_selector('div.alert.alert-success') }
	      it { should have_link('Sign out', href: signout_path) }
	      specify { expect(user.reload.name).to  eq new_name }
	      specify { expect(user.reload.email).to eq new_email }
	    end
	  end
	end

Note that Listing 9.9 adds the **sign_in** method from Listing 9.6 to the **before** block, which is required for the “Sign out” link test to pass, and also anticipates protecting the edit action from non-signed-in users (Section 9.2.1).

the **reload** method, which appears in the test for changing the user’s attributes:

	specify { expect(user.reload.name).to  eq new_name }
	specify { expect(user.reload.email).to eq new_email }

This reloads the user variable from the test database using **user.reload**, and then verifies that the user’s new name and email match the new values.

The update action needed to get the tests in Listing 9.9 to pass is similar to the final form of the create action (Listing 8.27), as seen in Listing 9.10. All this does is add

	flash[:success] = "Profile updated"
	redirect_to @user

to the code in Listing 9.8.

	Listing 9.10: The user update action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def update
	    @user = User.find(params[:id])
	    if @user.update_attributes(user_params)
	      flash[:success] = "Profile updated"
	      redirect_to @user
	    else
	      render 'edit'
	    end
	  end
	  .
	  .
	  .
	end

With the code in this section, the user edit page should be working, as you can double-check by re-running the test suite, which should now be green:

	$ bundle exec rspec spec/

# 9.2 - Authorization
**authentication** allows us to identify users of our site, and **authorization** lets us control what they can do.

Although the edit and update actions from Section 9.1 are functionally complete, they suffer from a ridiculous security flaw: *they allow anyone (even non-signed-in users) to access either action*, and *any signed-in user can update the information for any other user*. In this section, we’ll implement a security model that *requires users to be signed in* and *prevents them from updating any information other than their own*. Users *who aren’t signed in and who try to access protected pages will be forwarded to the signin page with a helpful message*

## 9.2.1 - Requiring signed-in users
Since the security restrictions for the **edit** and **update** actions are identical, we’ll handle them in a single RSpec describe block. Starting with the sign-in requirement, our initial tests verify that non-signed-in users attempting to access either action are simply sent to the signin page, as seen in Listing 9.11.

	Listing 9.11: Testing that the edit and update actions are protected.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "authorization" do

	    describe "for non-signed-in users" do
	      let(:user) { FactoryGirl.create(:user) }

	      describe "in the Users controller" do

	        describe "visiting the edit page" do
	          before { visit edit_user_path(user) }
	          it { should have_title('Sign in') }
	        end

	        describe "submitting to the update action" do
	          before { patch user_path(user) }
	          specify { expect(response).to redirect_to(signin_path) }
	        end
	      end
	    end
	  end
	end

The code in Listing 9.11 introduces a second way, apart from Capybara’s visit method, to access a controller action: by *issuing the appropriate HTTP request directly*, in this case using the **patch** method to issue a PATCH request:

	describe "submitting to the update action" do
	  before { patch user_path(user) }
	  specify { expect(response).to redirect_to(signin_path) }
	end

This issues a PATCH request directly to **/users/1**, which gets routed to the update action of the Users controller (Table 7.1). This is necessary because there is no way for a browser to visit the update action directly—it can only get there indirectly by submitting the edit form—so Capybara can’t do it either. But visiting the edit page only tests the authorization for the **edit** action, not for **update**. As a result, the only way to test the proper authorization for the update action itself is to issue a direct request. (As you might guess, in addition to patch Rails tests support **get**, **post**, and **delete** as well.)

When using one of the methods to issue HTTP requests directly, we get access to the low-level **response** object. Unlike the Capybara page object, **response** lets us test for the server response itself, in this case verifying that the update action responds by redirecting to the signin page:

	specify { expect(response).to redirect_to(signin_path) }

The authorization application code uses a before filter, which uses the `before_action` command to arrange for a particular method to be called before the given actions. (The command for before filters used to be called `before_filter`, but the Rails core team decided to rename it to emphasize that the filter takes place before particular controller actions.) To require users to be signed in, we define a **signed_in_user** method and invoke it using **before_action :signed_in_user**, as shown in Listing 9.12.

	Listing 9.12: Adding a signed_in_user before filter.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:edit, :update]
	  .
	  .
	  .
	  private

	    def user_params
	      params.require(:user).permit(:name, :email, :password,
	                                   :password_confirmation)
	    end

	    # Before filters

	    def signed_in_user
	      redirect_to signin_url, notice: "Please sign in." unless signed_in?
	    end
	end

By default, before filters apply to every action in a controller, so here we restrict the filter to act only on the **:edit** and **:update** actions by passing the appropriate **:only** options hash.

Note that Listing 9.12 uses a shortcut for setting **flash[:notice]** by passing an options hash to the **redirect_to** function. The code in Listing 9.12 is equivalent to the more verbose

	unless signed_in?
	  flash[:notice] = "Please sign in."
	  redirect_to signin_url
	end

(Unfortunately, the same construction doesn’t work for the **:error** or **:success** keys.)

Together with **:success** and **:error**, the :notice key completes our triumvirate of flash styles, all of which are supported natively by Bootstrap CSS. By signing out and attempting to access the user edit page **/users/1/edit**, we can see the resulting yellow “notice” box.

At this point, our test suite should be green:

	$ bundle exec rspec spec/

## 9.2.2 - Requiring the right user
Of course, requiring users to sign in isn’t quite enough; users should only be allowed to edit their own information. We can test for this by first signing in as an incorrect user and then hitting the edit and update actions (Listing 9.13). Note that, because we’re *not using Capybara for these tests* (no_capybara: true), we use the *get and patch methods to hit the edit and update actions directly*. In addition, because users should never even try to edit another user’s profile, upon detecting unauthorized access we *redirect to the root URL rather than to the signin page*.

	Listing 9.13: Testing that the edit and update actions require the right user.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "authorization" do
	    .
	    .
	    .
	    describe "as wrong user" do
	      let(:user) { FactoryGirl.create(:user) }
	      let(:wrong_user) { FactoryGirl.create(:user, email: "wrong@example.com") }
	      before { sign_in user, no_capybara: true }

	      describe "submitting a GET request to the Users#edit action" do
	        before { get edit_user_path(wrong_user) }
	        specify { expect(response.body).not_to match(full_title('Edit user')) }
	        specify { expect(response).to redirect_to(root_url) }
	      end

	      describe "submitting a PATCH request to the Users#update action" do
	        before { patch user_path(wrong_user) }
	        specify { expect(response).to redirect_to(root_url) }
	      end
	    end
	  end
	end

Note here that a factory can take an option:

	FactoryGirl.create(:user, email: "wrong@example.com")

This creates a user with a different email address from the default. The tests specify that the original user should not have access to the wrong user’s edit or update actions.

The application code adds a second before filter to call the **correct_user** method, as shown in Listing 9.14.

	Listing 9.14: A correct_user before filter to protect the edit/update pages.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:edit, :update]
	  before_action :correct_user,   only: [:edit, :update]
	  .
	  .
	  .
	  def edit
	  end

	  def update
	    if @user.update_attributes(user_params)
	      flash[:success] = "Profile updated"
	      redirect_to @user
	    else
	      render 'edit'
	    end
	  end
	  .
	  .
	  .
	  private

	    def user_params
	      params.require(:user).permit(:name, :email, :password,
	                                   :password_confirmation)
	    end

	    # Before filters

	    def signed_in_user
	      redirect_to signin_url, notice: "Please sign in." unless signed_in?
	    end

	    def correct_user
	      @user = User.find(params[:id])
	      redirect_to(root_url) unless current_user?(@user)
	    end
	end

The *correct_user* filter uses the **current_user?** boolean method, which we define in the Sessions helper (Listing 9.15).

	Listing 9.15: The current_user? method.
	app/helpers/sessions_helper.rb
	 module SessionsHelper
	  .
	  .
	  .
	  def current_user
	    remember_token = User.digest(cookies[:remember_token])
	    @current_user ||= User.find_by(remember_token: remember_token)
	  end

	  def current_user?(user)
	    user == current_user
	  end
	  .
	  .
	  .
	end

Listing 9.14 also shows the updated edit and update actions. Before, in Listing 9.2, we had

	def edit
	  @user = User.find(params[:id])
	end

and similarly for update. Now that the **correct_user** before filter defines **@user**, we can omit it from both actions.

Before moving on, you should verify that the test suite passes:

	$ bundle exec rspec spec/

## 9.2.3 - Friendly forwarding
Our site authorization is complete as written, but there is one minor blemish: when users try to access a protected page, they are currently redirected to their profile pages regardless of where they were trying to go. In other words, if a non-logged-in user tries to visit the edit page, after signing in the user will be redirected to **/users/1** instead of **/users/1/edit**. It would be much friendlier to *redirect them to their intended destination instead*.

To test for such “friendly forwarding”, we first visit the user edit page, which redirects to the signin page. We then enter valid signin information and click the “Sign in” button. The resulting page, which by default is the user’s profile, should in this case be the “Edit user” page. The test for this sequence appears in Listing 9.16.

	Listing 9.16: A test for friendly forwarding.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "authorization" do

	    describe "for non-signed-in users" do
	      let(:user) { FactoryGirl.create(:user) }

	      describe "when attempting to visit a protected page" do
	        before do
	          visit edit_user_path(user)
	          fill_in "Email",    with: user.email
	          fill_in "Password", with: user.password
	          click_button "Sign in"
	        end

	        describe "after signing in" do

	          it "should render the desired protected page" do
	            expect(page).to have_title('Edit user')
	          end
	        end
	      end
	      .
	      .
	      .
	    end
	    .
	    .
	    .
	  end
	end

Now for the implementation. In order to forward users to their intended destination, we need to store the location of the requested page somewhere, and then redirect to that location instead. We accomplish this with a pair of methods, `store_location` and `redirect_back_or`, both defined in the Sessions helper (Listing 9.17).

	Listing 9.17: Code to implement friendly forwarding.
	app/helpers/sessions_helper.rb
	 module SessionsHelper
	  .
	  .
	  .
	  def redirect_back_or(default)
	    redirect_to(session[:return_to] || default)
	    session.delete(:return_to)
	  end

	  def store_location
	    session[:return_to] = request.url if request.get?
	  end
	end

The storage mechanism is the **session** facility provided by Rails, which you can think of as being like an instance of the **cookies** variable from Section 8.2.1 that *automatically expires upon browser close*. We also use the request object to get the url, i.e., the URL of the requested page. The `store_location` method puts the requested URL in the session variable under the key **:return_to**, but only for a **GET** request (**if request.get?**). This prevents storing the forwarding URL if a user, say, submits a form when not logged in (which is an edge case but could happen if, e.g., a user deleted the remember token by hand before submitting the form); in this case, the resulting redirect would issue a GET request to a URL expecting POST, PATCH, or DELETE, thereby causing an error.

To make use of `store_location`, we need to add it to the `signed_in_user` before filter, as shown in Listing 9.18.

	Listing 9.18: Adding store_location to the signed-in user before filter.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:edit, :update]
	  before_action :correct_user,   only: [:edit, :update]
	  .
	  .
	  .
	  def edit
	  end
	  .
	  .
	  .
	  private

	    def user_params
	      params.require(:user).permit(:name, :email, :password,
	                                   :password_confirmation)
	    end

	    # Before filters

	    def signed_in_user
	      unless signed_in?
	        store_location
	        redirect_to signin_url, notice: "Please sign in."
	      end
	    end

	    def correct_user
	      @user = User.find(params[:id])
	      redirect_to(root_url) unless current_user?(@user)
	    end
	end

To implement the forwarding itself, we use the **redirect_back_or** method to redirect to the requested URL if it exists, or some default URL otherwise, which we add to the Sessions controller create action to redirect after successful signin (Listing 9.19). The **redirect_back_or** method uses the or operator `||` through

	session[:return_to] || default

This evaluates to **session[:return_to]** unless it’s **nil**, in which case it evaluates to the given default URL. Note that Listing 9.17 is *careful to remove the forwarding URL*; otherwise, subsequent signin attempts would forward to the protected page until the user closed their browser. (Testing for this is left as an exercise (Section 9.6).)

	Listing 9.19: The Sessions create action with friendly forwarding.
	app/controllers/sessions_controller.rb
	 class SessionsController < ApplicationController
	  .
	  .
	  .
	  def create
	    user = User.find_by(email: params[:session][:email].downcase)
	    if user && user.authenticate(params[:session][:password])
	      sign_in user
	      redirect_back_or user
	    else
	      flash.now[:error] = 'Invalid email/password combination'
	      render 'new'
	    end
	  end
	  .
	  .
	  .
	end

(If you completed the first exercise in Chapter 8, be sure to use the proper params hash in Listing 9.19.)

With that, the friendly forwarding integration test in Listing 9.16 should pass, and the basic user authentication and page protection implementation is complete. As usual, it’s a good idea to verify that the test suite is green before proceeding:

	$ bundle exec rspec spec/

# 9.3 - Showing all users
In this section, we’ll add the *penultimate* user action, the **index** action, which is designed to display all the users instead of just one. Along the way, we’ll learn about populating the database with sample users and *paginating the user output* so that the index page can scale up to *display a potentially large number of users*. A mockup of the result—users, pagination links, and a “Users” navigation link—appears in Figure 9.7.6 In Section 9.4, we’ll add an administrative interface to the user index so that (*presumably troublesome*) users can be destroyed.

<figure>
  <figcaption style="text-align:center;">Figure 9.7: A mockup of the user index, with pagination and a “Users” nav link.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/user_index_mockup_bootstrap.png" alt="user index mockup" title="user index mockup">
</figure>

## 9.3.1 - User index
We’ll start by testing that the **index** action is protected by visiting the **users_path** (Table 7.1) and verifying that we are redirected to the signin page. As with other authorization tests, we’ll put this example in the authentication integration test, as shown in Listing 9.20.

	Listing 9.20: Testing that the index action is protected.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "authorization" do

	    describe "for non-signed-in users" do
	      .
	      .
	      .
	      describe "in the Users controller" do
	        .
	        .
	        .
	        describe "visiting the user index" do
	          before { visit users_path }
	          it { should have_title('Sign in') }
	        end
	      end
	      .
	      .
	      .
	    end
	  end
	end

The corresponding application code simply involves adding **index** to the list of actions protected by the `signed_in_user` before filter, as shown in Listing 9.21.

	Listing 9.21: Requiring a signed-in user for the index action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:index, :edit, :update]
	  before_action :correct_user,   only: [:edit, :update]

	  def index
	  end

	  def show
	    @user = User.find(params[:id])
	  end
	  .
	  .
	  .
	end

The next set of tests makes sure that, for signed-in users, the index page has the *right title/content and lists all of the site’s users*. The method is to make three factory users (signing in as the first one) and then verify that the index page has a list element (li) tag for the name of each one. Note that we’ve taken care to give the users different names so that each element in the list of users has a unique entry, as shown in Listing 9.22.

	Listing 9.22: Tests for the user index page.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do

	  subject { page }

	  describe "index" do
	    before do
	      sign_in FactoryGirl.create(:user)
	      FactoryGirl.create(:user, name: "Bob", email: "bob@example.com")
	      FactoryGirl.create(:user, name: "Ben", email: "ben@example.com")
	      visit users_path
	    end

	    it { should have_title('All users') }
	    it { should have_content('All users') }

	    it "should list each user" do
	      User.all.each do |user|
	        expect(page).to have_selector('li', text: user.name)
	      end
	    end
	  end
	  .
	  .
	  .
	end

As you may recall from the corresponding action in the demo app (Listing 2.4), the application code uses **User.all** to pull all the users out of the database, assigning them to an **@users** instance variable for use in the view, as seen in Listing 9.23. (If displaying all the users at once seems like a bad idea, you’re right, and we’ll remove this blemish in Section 9.3.3.)

	Listing 9.23: The user index action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:index, :edit, :update]
	  .
	  .
	  .
	  def index
	    @users = User.all
	  end
	  .
	  .
	  .
	end

To make the actual index page, we need to make a view that iterates through the users and wraps each one in an **li** tag. We do this with the each method, displaying each user’s Gravatar and name, while wrapping the whole thing in an unordered list (**ul**) tag (Listing 9.24). The code in Listing 9.24 uses the result of Listing 7.30 from Section 7.6, which allows us to pass an option to the *Gravatar helper specifying a size* other than the default. If you didn’t do that exercise, update your Users helper file with the contents of Listing 7.30 before proceeding.

	Listing 9.24: The user index view.
	app/views/users/index.html.erb
	 <% provide(:title, 'All users') %>
	<h1>All users</h1>

	<ul class="users">
	  <% @users.each do |user| %>
	    <li>
	      <%= gravatar_for user, size: 52 %>
	      <%= link_to user.name, user %>
	    </li>
	  <% end %>
	</ul>

Let’s also add a little CSS (or, rather, SCSS) for style (Listing 9.25).

	Listing 9.25: CSS for the user index.
	app/assets/stylesheets/custom.css.scss
	 .
	.
	.

	/* Users index */

	.users {
	  list-style: none;
	  margin: 0;
	  li {
	    overflow: auto;
	    padding: 10px 0;
	    border-top: 1px solid $grayLighter;
	    &:last-child {
	      border-bottom: 1px solid $grayLighter;
	    }
	  }
	}

Finally, we’ll add the URL to the users link in the site’s navigation header using users_path, thereby using the last of the unused named routes in Table 7.1. The test (Listing 9.26) and application code (Listing 9.27) are both straightforward.

	Listing 9.26: A test for the “Users” link URL.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	    .
	    .
	    .
	    describe "with valid information" do
	      let(:user) { FactoryGirl.create(:user) }
	      before { sign_in user }

	      it { should have_title(user.name) }
	      it { should have_link('Users',       href: users_path) }
	      it { should have_link('Profile',     href: user_path(user)) }
	      it { should have_link('Settings',    href: edit_user_path(user)) }
	      it { should have_link('Sign out',    href: signout_path) }
	      it { should_not have_link('Sign in', href: signin_path) }
	      .
	      .
	      .
	    end
	  end
	end

	Listing 9.27: Adding the URL to the users link.
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
	            <li><%= link_to "Users", users_path %></li>
	            <li id="fat-menu" class="dropdown">
	              <a href="#" class="dropdown-toggle" data-toggle="dropdown">
	                Account <b class="caret"></b>
	              </a>
	              <ul class="dropdown-menu">
	                <li><%= link_to "Profile", current_user %></li>
	                <li><%= link_to "Settings", edit_user_path(current_user) %></li>
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

With that, the user index is fully functional, with all tests passing:

	$ bundle exec rspec spec/

## 9.3.2 - Sample users
In this section, we’ll give our lonely sample user some company. Of course, to create enough users to make a decent user index, we could use our web browser to visit the signup page and make the new users one by one, but far a better solution is to use **Ruby (and Rake)** to make the users for us.

First, we’ll add the **Faker** gem to the Gemfile, which will allow us to make sample users with semi-realistic names and email addresses (Listing 9.28).

	Listing 9.28: Adding the Faker gem to the Gemfile.
	source 'https://rubygems.org'
	ruby '2.0.0'
	#ruby-gemset=railstutorial_rails_4_0

	gem 'rails', '4.0.8'
	gem 'bootstrap-sass', '2.3.2.0'
	gem 'sprockets', '2.11.0'
	gem 'bcrypt-ruby', '3.1.2'
	gem 'faker', '1.1.2'
	.
	.
	.

Then install as usual:

	$ bundle install

Next, we’ll add a **Rake task** to create sample users. Rake tasks live in the **lib/tasks** directory, and are defined using **namespaces** (in this case, **:db**), as seen in Listing 9.29. (This is a bit advanced, so don’t worry too much about the details.)

	Listing 9.29: A Rake task for populating the database with sample users.
	lib/tasks/sample_data.rake
	 namespace :db do
	  desc "Fill database with sample data"
	  task populate: :environment do
	    User.create!(name: "Example User",
	                 email: "example@railstutorial.org",
	                 password: "foobar",
	                 password_confirmation: "foobar")
	    99.times do |n|
	      name  = Faker::Name.name
	      email = "example-#{n+1}@railstutorial.org"
	      password  = "password"
	      User.create!(name: name,
	                   email: email,
	                   password: password,
	                   password_confirmation: password)
	    end
	  end
	end

This defines a **task db:populate** that creates an example user with name and email address replicating our previous one, and then makes 99 more. The line

	task populate: :environment do

*ensures that the Rake task has access to the local Rails environment*, *including the User model* (and hence User.create!). Here **create!** is just like the create method, except it *raises an exception* (Section 6.1.4) for an invalid user rather than returning false. This noisier construction makes debugging easier by avoiding silent errors.

With the **:db** namespace as in Listing 9.29, we can invoke the Rake task as follows:

	$ bundle exec rake db:reset
	$ bundle exec rake db:populate
	$ bundle exec rake test:prepare

## 9.3.3 - Pagination
There are several pagination methods in Rails; we’ll use one of the simplest and most robust, called `will_paginate`. To use it, we need to include both the `will_paginate` gem and `bootstrap-will_paginate`, which configures will_paginate to use Bootstrap’s pagination styles. The updated Gemfile appears in Listing 9.30.

	Listing 9.30: Including will_paginate in the Gemfile.
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
	.
	.
	.

Then run bundle install:

	$ bundle install

You should also restart the web server to ensure that the new gems are loaded properly.

Because the `will_paginate` gem is in wide use, there’s no need to test it thoroughly, so we’ll take a lightweight approach. First, we’ll test for a **div** with CSS class “pagination”, which is what gets output by will_paginate. Then we’ll verify that the *correct users appear on the first page of results*. This requires the use of the paginate method, which we’ll cover shortly.

As before, we’ll use Factory Girl to simulate users, but immediately we have a problem: user email addresses must be unique, which would appear to require creating more than 30 users by hand—a terribly *cumbersome* job. In addition, when testing for user listings it would be convenient for them all to have different names. Fortunately, Factory Girl anticipates this issue, and provides sequences to solve it. Our original factory (Listing 7.8) hard-coded the name and email address:

	FactoryGirl.define do
	  factory :user do
	    name     "Michael Hartl"
	    email    "michael@example.com"
	    password "foobar"
	    password_confirmation "foobar"
	  end
	end

Instead, we can arrange for a sequence of names and email addresses using the sequence method:

	factory :user do
	  sequence(:name)  { |n| "Person #{n}" }
	  sequence(:email) { |n| "person_#{n}@example.com"}
	  .
	  .
	  .

Here sequence takes a symbol corresponding to the desired attribute (such as :name) and a block with one variable, which we have called n. Upon successive invocations of the FactoryGirl method,

	FactoryGirl.create(:user)

The block variable n is automatically incremented, so that the first user has name “Person 1” and email address `“person_1@example.com”`, the second user has name “Person 2” and email address “person_2@example.com”, and so on. The full code appears in Listing 9.31.

	Listing 9.31: Defining a Factory Girl sequence.
	spec/factories.rb
	 FactoryGirl.define do
	  factory :user do
	    sequence(:name)  { |n| "Person #{n}" }
	    sequence(:email) { |n| "person_#{n}@example.com"}
	    password "foobar"
	    password_confirmation "foobar"
	  end
	end

Applying the idea of factory sequences, we can make 30 users in our test, which (as we will see) will be sufficient to invoke pagination:

	before(:all) { 30.times { FactoryGirl.create(:user) } }
	after(:all)  { User.delete_all }

Note here the use of **before(:all)**, which ensures that the sample users are created once, before all the tests in the block. This is an optimization for speed, as creating 30 users can be slow on some systems. We use the complementary method after(:all) to delete the users once we’re done.

The tests for the appearance of the pagination div and the right users appears in Listing 9.32. Note the replacement of the User.all array from Listing 9.22 with User.paginate(page: 1), which (as we’ll see momentarily) is how to pull out the first page of users from the database. Note also that Listing 9.32 uses before(:each) to emphasize the contrast with before(:all).

	Listing 9.32: Tests for pagination.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do

	  subject { page }

	  describe "index" do
	    let(:user) { FactoryGirl.create(:user) }
	    before(:each) do
	      sign_in user
	      visit users_path
	    end

	    it { should have_title('All users') }
	    it { should have_content('All users') }

	    describe "pagination" do

	      before(:all) { 30.times { FactoryGirl.create(:user) } }
	      after(:all)  { User.delete_all }

	      it { should have_selector('div.pagination') }

	      it "should list each user" do
	        User.paginate(page: 1).each do |user|
	          expect(page).to have_selector('li', text: user.name)
	        end
	      end
	    end
	  end
	  .
	  .
	  .
	end

To get pagination working, we need to add some code to the **index** view telling Rails to paginate the users, and we need to replace **User.all** in the index action with an object that knows about pagination. We’ll start by adding the special will_paginate method in the view (Listing 9.33); we’ll see in a moment why the code appears both above and below the user list.

	Listing 9.33: The user index with pagination.
	app/views/users/index.html.erb
	 <% provide(:title, 'All users') %>
	<h1>All users</h1>

	<%= will_paginate %>

	<ul class="users">
	  <% @users.each do |user| %>
	    <li>
	      <%= gravatar_for user, size: 52 %>
	      <%= link_to user.name, user %>
	    </li>
	  <% end %>
	</ul>

	<%= will_paginate %>

The `will_paginate` method is a little magical; inside a users view, it automatically looks for an **@users** object, and then displays pagination links to access other pages. The view in Listing 9.33 doesn’t work yet, though, because currently **@users** contains the results of User.all (Listing 9.23), whereas will_paginate requires that we paginate the results explicitly using the paginate method:

	$ rails console
	>> User.paginate(page: 1)
	  User Load (1.5ms)  SELECT "users".* FROM "users" LIMIT 30 OFFSET 0
	   (1.7ms)  SELECT COUNT(*) FROM "users"
	=> #<ActiveRecord::Relation [#<User id: 1,...

Note that paginate takes a hash argument with key :page and value equal to the page requested. User.paginate pulls the users out of the database one chunk at a time (30 by default), based on the :page parameter. So, for example, page 1 is users 1–30, page 2 is users 31–60, etc. If the page is nil, paginate simply returns the first page.

Using the paginate method, we can paginate the users in the sample application by using paginate in place of all in the index action (Listing 9.34). Here the :page parameter comes from **params[:page]**, which is generated automatically by will_paginate.

	Listing 9.34: Paginating the users in the index action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:index, :edit, :update]
	  .
	  .
	  .
	  def index
	    @users = User.paginate(page: params[:page])
	  end
	  .
	  .
	  .
	end

The user index page should now be working, appearing as in Figure 9.10. (On some systems, you may have to restart the Rails server at this point.) Because we included will_paginate both above and below the user list, the pagination links appear in both places.

## 9.3.4 - Partial refactoring
The paginated user index is now complete, but there’s one improvement *I can’t resist including*: Rails has some *incredibly slick tools* for making compact views, and in this section we’ll refactor the index page to use them. Because our code is well-tested, we can refactor with confidence, assured that we are unlikely to break our site’s functionality.

The first step in our refactoring is to replace the user **li** from Listing 9.33 with a **render** call (Listing 9.35).

	Listing 9.35: The first refactoring attempt at the index view.
	app/views/users/index.html.erb
	 <% provide(:title, 'All users') %>
	<h1>All users</h1>

	<%= will_paginate %>

	<ul class="users">
	  <% @users.each do |user| %>
	    <%= render user %>
	  <% end %>
	</ul>

	<%= will_paginate %>

Here *we call render not on a string with the name of a partial*, but rather *on a user variable of class User*; in this context, Rails automatically looks for a partial called **_user.html.erb**, which we must create (Listing 9.36).

	Listing 9.36: A partial to render a single user.
	app/views/users/_user.html.erb
	 <li>
	  <%= gravatar_for user, size: 52 %>
	  <%= link_to user.name, user %>
	</li>

This is a definite improvement, but we can do even better: we can call render directly on the **@users** variable (Listing 9.37).

	Listing 9.37: The fully refactored user index.
	app/views/users/index.html.erb
	 <% provide(:title, 'All users') %>
	<h1>All users</h1>

	<%= will_paginate %>

	<ul class="users">
	  <%= render @users %>
	</ul>

	<%= will_paginate %>

Here Rails infers that @users is a list of User objects; moreover, when called with a collection of users, Rails automatically iterates through them and renders each one with the **_user.html.erb** partial. The result is the impressively compact code in Listing 9.37. As with any refactoring, you should verify that the test suite is still green after changing the application code:

	$ bundle exec rspec spec/


# 9.4 - Deleting users
Now that the user index is complete, there’s only one canonical REST action left: **destroy**. In this section, we’ll add links to delete users, and define the **destroy** action necessary to accomplish the deletion. But first, we’ll create the *class of administrative users authorized to do so.*


## 9.4.1 - Administrative users
We will identify privileged administrative users with a boolean **admin** attribute in the User model, which, as we’ll see, will automatically lead to an **admin?** boolean method to test for admin status. We can write tests for this attribute as in Listing 9.38.

	Listing 9.38: Tests for an admin attribute.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do
	  .
	  .
	  .
	  it { should respond_to(:authenticate) }
	  it { should respond_to(:admin) }

	  it { should be_valid }
	  it { should_not be_admin }

	  describe "with admin attribute set to 'true'" do
	    before do
	      @user.save!
	      @user.toggle!(:admin)
	    end

	    it { should be_admin }
	  end
	  .
	  .
	  .
	end

Here we’ve used the **toggle!** method to flip the admin attribute from false to true. Also note that the line

	it { should be_admin }

implies (via the RSpec boolean convention) that the user should have an **admin?** boolean method.

As usual, we add the admin attribute with a migration, indicating the boolean type on the command line:

	$ rails generate migration add_admin_to_users admin:boolean

The migration simply adds the admin column to the users table (Listing 9.39), yielding the data model in Figure 9.13.

	Listing 9.39: The migration to add a boolean admin attribute to users.
	db/migrate/[timestamp]_add_admin_to_users.rb
	 class AddAdminToUsers < ActiveRecord::Migration
	  def change
	    add_column :users, :admin, :boolean, default: false
	  end
	end

Note that we’ve added the argument **default: false** to **add_column** in Listing 9.39, which means that users will not be administrators by default. (Without the default: false argument, admin will be **nil** by default, which is still false, so this step is not strictly necessary. It is more explicit, though, and communicates our intentions more clearly both to Rails and to readers of our code.)

Finally, we migrate the development database and prepare the test database:

	$ bundle exec rake db:migrate
	$ bundle exec rake test:prepare

As expected, Rails figures out the boolean nature of the admin attribute and automatically adds the question-mark method admin?:

	$ rails console --sandbox
	>> user = User.first
	>> user.admin?
	=> false
	>> user.toggle!(:admin)
	=> true
	>> user.admin?
	=> true

As a result, the admin tests should pass:

	$ bundle exec rspec spec/models/user_spec.rb

As a final step, let’s update our sample data populator to make the first user an admin by default (Listing 9.40).

	Listing 9.40: The sample data populator code with an admin user.
	lib/tasks/sample_data.rake
	 namespace :db do
	  desc "Fill database with sample data"
	  task populate: :environment do
	    admin = User.create!(name: "Example User",
	                         email: "example@railstutorial.org",
	                         password: "foobar",
	                         password_confirmation: "foobar",
	                         admin: true)
	    .
	    .
	    .
	  end
	end

Then reset the database and re-populate the sample data:

	$ bundle exec rake db:reset
	$ bundle exec rake db:populate
	$ bundle exec rake test:prepare

### Revisiting strong parameters

You might have noticed that Listing 9.40 makes the user an admin by including **admin: true** in the initialization hash. This underscores the danger of exposing our objects to the wild Web: if we simply passed an initialization hash in from an arbitrary web request, a malicious user could send a PATCH request as follows:8

	patch /users/17?admin=1

This request would make user 17 an admin, which would be a potentially serious security breach, to say the least.

Because of this danger, it is essential to pass parameters that have been processed to permit only safe-to-edit attributes. As noted in Section 7.3.2, this is accomplished using strong parameters by calling require and permit on the params hash:

    def user_params
      params.require(:user).permit(:name, :email, :password,
                                   :password_confirmation)
    end

Note in particular that **admin** is not in the list of permitted attributes. This is what prevents arbitrary users from granting themselves administrative access to our application. Because of its importance, it’s a good idea to write a test for any attribute that isn’t editible, and writing such a test for the **admin** attribute is left as an exercise (Section 9.6).


## 9.4.2 - The destroy action
The final step needed to complete the Users resource is to add delete links and a **destroy** action. We’ll start by adding a delete link for each user on the user index page, restricting access to administrative users.

To write tests for the delete functionality, it’s helpful to be able to have a factory to create admins. We can accomplish this by adding an :admin block to our factories, as shown in Listing 9.41.

	Listing 9.41: Adding a factory for administrative users.
	spec/factories.rb
	 FactoryGirl.define do
	  factory :user do
	    sequence(:name)  { |n| "Person #{n}" }
	    sequence(:email) { |n| "person_#{n}@example.com"}
	    password "foobar"
	    password_confirmation "foobar"

	    factory :admin do
	      admin true
	    end
	  end
	end

With the code in Listing 9.41, we can now use **FactoryGirl.create(:admin)** to create an administrative user in our tests.

Our security model requires that ordinary users not see delete links:

	it { should_not have_link('delete') }

But administrative users should see such links, and by clicking on a delete link we expect an admin to delete the user, i.e., to change the User count by -1:

	it { should have_link('delete', href: user_path(User.first)) }
	it "should be able to delete another user" do
	  expect do
	    click_link('delete', match: :first)
	  end.to change(User, :count).by(-1)
	end
	it { should_not have_link('delete', href: user_path(admin)) }

This includes the code **match: :first**, which tells Capybara that we don’t care which delete link it clicks; it should just click the first one it sees. Note also that we have added a test to verify that the admin does not see a link to delete himself. The full set of delete link tests appears in Listing 9.42.

	Listing 9.42: Tests for delete links.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do

	  subject { page }

	  describe "index" do

	    let(:user) { FactoryGirl.create(:user) }

	    before do
	      sign_in user
	      visit users_path
	    end

	    it { should have_title('All users') }
	    it { should have_content('All users') }

	    describe "pagination" do
	      .
	      .
	      .
	    end

	    describe "delete links" do

	      it { should_not have_link('delete') }

	      describe "as an admin user" do
	        let(:admin) { FactoryGirl.create(:admin) }
	        before do
	          sign_in admin
	          visit users_path
	        end

	        it { should have_link('delete', href: user_path(User.first)) }
	        it "should be able to delete another user" do
	          expect do
	            click_link('delete', match: :first)
	          end.to change(User, :count).by(-1)
	        end
	        it { should_not have_link('delete', href: user_path(admin)) }
	      end
	    end
	  end
	  .
	  .
	  .
	end

The application code links to "delete" if the current user is an admin (Listing 9.43). Note the **method: :delete** argument, which arranges for the link to issue the necessary DELETE request. We’ve also wrapped each link inside an if statement so that only admins can see them. The result for our admin user appears in Figure 9.14.

	Listing 9.43: User delete links (viewable only by admins).
	app/views/users/_user.html.erb
	 <li>
	  <%= gravatar_for user, size: 52 %>
	  <%= link_to user.name, user %>
	  <% if current_user.admin? && !current_user?(user) %>
	    | <%= link_to "delete", user, method: :delete,
	                                  data: { confirm: "You sure?" } %>
	  <% end %>
	</li>

Web browsers can’t send DELETE requests natively, so Rails fakes them with JavaScript. This means that the delete links won’t work if the user has JavaScript disabled. If you must support non-JavaScript-enabled browsers you can *fake a DELETE request using a form and a POST request*, which works even without JavaScript; see the RailsCast on “[Destroy Without JavaScript](http://railscasts.com/episodes/77-destroy-without-javascript)” for details.

To get the delete links to work, we need to add a **destroy** action (Table 7.1), which finds the corresponding user and destroys it with the Active Record destroy method, finally redirecting to the user index, as seen in Listing 9.44. Note that we also add **:destroy** to the `signed_in_user` before filter.

	Listing 9.44: Adding a working destroy action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:index, :edit, :update, :destroy]
	  before_action :correct_user,   only: [:edit, :update]
	  .
	  .
	  .
	  def destroy
	    User.find(params[:id]).destroy
	    flash[:success] = "User deleted."
	    redirect_to users_url
	  end
	  .
	  .
	  .
	end

Note that the destroy action uses method chaining to combine the find and destroy into one line:

	User.find(params[:id]).destroy

As constructed, only **admins** can destroy users through the web, because only admins can see the delete links. Unfortunately, there’s still a terrible security hole: any sufficiently sophisticated attacker could simply issue DELETE requests directly from the command line to delete any user on the site. To secure the site properly, we also need access control on the destroy action, so our tests should check not only that admins can delete users, but also that *other users can’t*. The results appear in Listing 9.45. Note that, in analogy with the patch method from Listing 9.11, we use delete to issue a DELETE request directly to the specified URL (in this case, the user path, as required by Table 7.1).

	Listing 9.45: A test for protecting the destroy action.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "authorization" do
	    .
	    .
	    .
	    describe "as non-admin user" do
	      let(:user) { FactoryGirl.create(:user) }
	      let(:non_admin) { FactoryGirl.create(:user) }

	      before { sign_in non_admin, no_capybara: true }

	      describe "submitting a DELETE request to the Users#destroy action" do
	        before { delete user_path(user) }
	        specify { expect(response).to redirect_to(root_url) }
	      end
	    end
	  end
	end

In principle, there’s still a minor security hole, which is that an admin could delete himself by issuing a DELETE request directly. One might argue that such an admin is only getting what they deserve, but it would be nice to prevent such an occurrence, and doing so is left as an exercise (Section 9.6).

As you *might suspect by now*, the application code uses a before filter, this time to *restrict access to the destroy action to admins*. The resulting **admin_user** before filter appears in Listing 9.46.

	Listing 9.46: A before filter restricting the destroy action to admins.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  before_action :signed_in_user, only: [:index, :edit, :update, :destroy]
	  before_action :correct_user,   only: [:edit, :update]
	  before_action :admin_user,     only: :destroy
	  .
	  .
	  .
	  private
	    .
	    .
	    .
	    def admin_user
	      redirect_to(root_url) unless current_user.admin?
	    end
	end

At this point, all the tests should be passing, and the Users resource—with its controller, model, and views—is functionally complete.

	$ bundle exec rspec spec/

# 9.5 - Conclusion
We’ve come a long way since introducing the Users controller way back in Section 5.4. Those users couldn’t even sign up; now users can sign up, sign in, sign out, view their profiles, edit their settings, and see an index of all users—and some can even destroy other users.

The rest of this book builds on the foundation of the Users resource (and associated authorization system) to make a site with Twitter-like microposts (Chapter 10) and a status feed of posts from followed users (Chapter 11). These chapters will introduce some of the most powerful features of Rails, including data modeling with `has_many` and `has_many through`.

Before moving on, be sure to merge all the changes into the master branch:

	$ git add .
	$ git commit -m "Finish user edit, update, index, and destroy actions"
	$ git checkout master
	$ git merge updating-users

You can also deploy the application and even populate the production database with sample users (using the pg:reset task to reset the production database):

	$ git push heroku
	$ heroku pg:reset DATABASE
	$ heroku run rake db:migrate
	$ heroku run rake db:populate

To get the changes to show up, you may have to force an app restart at Heroku:

	$ heroku restart

It’s also worth noting that this chapter saw the last of the necessary gem installations. For reference, the final Gemfile is shown in Listing 9.47. (Optional gems may be system-dependent and are commented out. You can uncomment them to see if they work on your system.)

	Listing 9.47: The final Gemfile for the sample application.
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

# 9.6 - Exercises

