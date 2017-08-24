[TOC]

Add a second full resource: user **microposts**. These are short messages associated with a particular user. Constructing the Micropost data model, associating it with the User model using the `has_many` and `belongs_to` methods, and then making the forms and partials needed to manipulate and display the results. In Chapter 11, we’ll complete our tiny Twitter clone by adding the notion of following users in order to receive a feed of their **microposts**.

If you’re using Git for version control, I suggest making a topic branch as usual:

	$ git checkout -user-microposts

# 10.1 - A Micropost model
What follows builds on the work from Section 2.3; as with the model in that section, our new Micropost model will include data **validations** and an **association** with the User model. Unlike that model, the present Micropost model will be fully tested, and will also have a default **ordering** and automatic **destruction** if its parent user is destroyed.

## 10.1.1 - The basic model
The Micropost model needs only two attributes: a **content** attribute to hold the micropost’s content, and a **user_id** to associate a micropost with a particular user. As with the case of the User model (Listing 6.1), we generate it using generate model:

	$ rails generate model Micropost content:string user_id:integer

It’s possible that this will generate a Micropost factory, which you should remove since we’ll be making one later by hand (Section 10.1.4):

	$ rm -f spec/factories/microposts.rb

The generate command produces a migration to create a microposts table in the database (Listing 10.1); compare it to the analogous migration for the users table from Listing 6.2.

	Listing 10.1: The Micropost migration. (Note the index on user_id and created_at.)
	db/migrate/[timestamp]_create_microposts.rb
	 class CreateMicroposts < ActiveRecord::Migration
	  def change
	    create_table :microposts do |t|
	      t.string :content
	      t.integer :user_id

	      t.timestamps
	    end
	    add_index :microposts, [:user_id, :created_at]
	  end
	end

Note that, since we expect to retrieve all the microposts associated with a given user id in reverse order of creation, Listing 10.1 adds an index (Box 6.2) on the `user_id` and `created_at` columns:

	add_index :microposts, [:user_id, :created_at]

By including both the `user_id` and `created_at` columns as an array, we arrange for Rails to create a *multiple key index*, which means that Active Record uses both keys at the same time. Note also the **t.timestamps** line, which (as mentioned in Section 6.1.1) adds the magic `created_at` and `updated_at` columns. We’ll put the created_at column to work in Section 10.1.4 and Section 10.2.1.

We’ll start with some minimal tests for the Micropost model based on the analogous tests for the User model (Listing 6.5). In particular, we verify that a micropost object responds to the content and user_id attributes, as shown in Listing 10.2.

	Listing 10.2: The initial Micropost spec.
	spec/models/micropost_spec.rb
	 require 'spec_helper'

	describe Micropost do

	  let(:user) { FactoryGirl.create(:user) }
	  before do
	    # This code is not idiomatically correct.
	    @micropost = Micropost.new(content: "Lorem ipsum", user_id: user.id)
	  end

	  subject { @micropost }

	  it { should respond_to(:content) }
	  it { should respond_to(:user_id) }
	end

We can get these tests to pass by running the microposts migration and preparing the test database:

	$ bundle exec rake db:migrate
	$ bundle exec rake test:prepare

You should verify that the tests pass:

	$ bundle exec rspec spec/models/micropost_spec.rb

Even though the tests are passing, you might have noticed this code:

	let(:user) { FactoryGirl.create(:user) }
	before do
	  # This code is not idiomatically correct.
	  @micropost = Micropost.new(content: "Lorem ipsum", user_id: user.id)
	end

The comment indicates that the code in the before block is not **idiomatically correct**. That is, it works, but it’s not the Rails way. See if you can guess why. We’ll see the answer in Section 10.1.3.

## 10.1.2 - The first validation
One of the necessary aspects of the Micropost model is the *presence of a user id* to indicate which user made the micropost. The *idiomatically correct way* to do this is to use **Active Record associations**, which we’ll implement in Section 10.1.3. Since this will involve a minor refactoring, in this section we’ll write a test to catch any future regressions.

As shown in Listing 10.3, the validation test for user id just sets the id to **nil** and then checks that the resulting micropost is invalid. (Compare with the User model tests in Listing 6.8.)

	Listing 10.3: Tests for the validity of a new micropost.
	spec/models/micropost_spec.rb
	 require 'spec_helper'

	describe Micropost do

	  let(:user) { FactoryGirl.create(:user) }
	  before do
	    # This code is not idiomatically correct.
	    @micropost = Micropost.new(content: "Lorem ipsum", user_id: user.id)
	  end

	  subject { @micropost }

	  it { should respond_to(:content) }
	  it { should respond_to(:user_id) }

	  it { should be_valid }

	  describe "when user_id is not present" do
	    before { @micropost.user_id = nil }
	    it { should_not be_valid }
	  end
	end

This code requires that the micropost be valid and tests for the presence of the user_id attribute. We can get these tests to pass with the simple presence validation shown in Listing 10.4.

	Listing 10.4: A validation for the micropost’s user_id.
	app/models/micropost.rb
	 class Micropost < ActiveRecord::Base
	  validates :user_id, presence: true
	end

## 10.1.3 - User/Micropost associations
When constructing data models for web applications, it is essential to be able to make **associations** between individual models. In the present case, each micropost is associated with one user, and each user is associated with (potentially) many microposts—a relationship seen briefly in Section 2.3.3 and shown *schematically* in Figure 10.2 and Figure 10.3. As part of implementing these associations, we’ll write tests for the Micropost model and add a couple of tests to the User model.

<figure>
  <figcaption style="text-align:center;">Figure 10.2: The belongs_to relationship between a micropost and its user.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/micropost_belongs_to_user.png" alt="association" title="association">
</figure>

<figure>
  <figcaption style="text-align:center;">Figure 10.3: The has_many relationship between a user and its microposts.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/user_has_many_microposts.png" alt="association" title="association">
</figure>

Using the `belongs_to`/`has_many` association defined in this section, Rails constructs the methods shown in Table 10.1.

Method	| Purpose
-|-
micropost.user	| Return the User object associated with the micropost.
user.microposts	| Return an array of the user’s microposts.
user.microposts.create(arg) |	Create a micropost (user_id = user.id).
user.microposts.create!(arg) |	Create a micropost (exception on failure).
user.microposts.build(arg)	| Return a new Micropost object (user_id = user.id).

Note from Table 10.1 that instead of

	Micropost.create
	Micropost.create!
	Micropost.new

we have

	user.microposts.create
	user.microposts.create!
	user.microposts.build

This pattern is the canonical way to make a micropost: through its association with a user. When a new micropost is made in this way, its user_id is automatically set to the right value. In particular, we can replace the code

	let(:user) { FactoryGirl.create(:user) }
	before do
	  # This code is not idiomatically correct.
	  @micropost = Micropost.new(content: "Lorem ipsum", user_id: user.id)
	end

from Listing 10.3 with

	let(:user) { FactoryGirl.create(:user) }
	before { @micropost = user.microposts.build(content: "Lorem ipsum") }

As seen in Table 10.1, another result of the user/micropost association is micropost.user, which simply returns the micropost’s user. We can test this with the it and its methods as follows:

	it { should respond_to(:user) }
	its(:user) { should eq user }

The resulting Micropost model tests are shown in Listing 10.5.

	Listing 10.5: Tests for the micropost’s user association.
	spec/models/micropost_spec.rb
	 require 'spec_helper'

	describe Micropost do

	  let(:user) { FactoryGirl.create(:user) }
	  before { @micropost = user.microposts.build(content: "Lorem ipsum") }

	  subject { @micropost }

	  it { should respond_to(:content) }
	  it { should respond_to(:user_id) }
	  it { should respond_to(:user) }
	  its(:user) { should eq user }

	  it { should be_valid }

	  describe "when user_id is not present" do
	    before { @micropost.user_id = nil }
	    it { should_not be_valid }
	  end
	end

On the User model side of the association, we’ll defer the more detailed tests to Section 10.1.4; for now, we’ll simply test for the presence of a microposts attribute (Listing 10.6).

	Listing 10.6: A test for the user’s microposts attribute.
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
	  it { should respond_to(:admin) }
	  it { should respond_to(:microposts) }
	  .
	  .
	  .
	end

After all that work, the code to implement the association is almost comically short: we can get the tests in both Listing 10.5 and Listing 10.6 to pass by adding just two lines: `belongs_to :user` (Listing 10.7) and `has_many :microposts` (Listing 10.8).

	Listing 10.7: A micropost belongs_to a user.
	app/models/micropost.rb
	 class Micropost < ActiveRecord::Base
	  belongs_to :user
	  validates :user_id, presence: true
	end

	Listing 10.8: A user has_many microposts.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  has_many :microposts
	  .
	  .
	  .
	end

At this point, you should compare the entries in Table 10.1 with the code in Listing 10.5 and Listing 10.6 to satisfy yourself that you understand the basic nature of the associations. You should also check that the tests pass:

	$ bundle exec rspec spec/models

## 10.1.4 - Micropost refinements
The test in Listing 10.6 of the has_many association doesn’t test for much—it merely verifies the existence of a microposts attribute. In this section, we’ll add **ordering** and **dependency** to microposts, while also testing that the *user.microposts method actually returns an array* of microposts.

We will need to construct some microposts in the User model test, which means that we should make a micropost factory at this point. To do this, we need a way to make an association in Factory Girl. Happily, this is easy, as seen in Listing 10.9.

	Listing 10.9: The complete factory file, including a new factory for microposts.
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

	  factory :micropost do
	    content "Lorem ipsum"
	    user
	  end
	end

Here we tell Factory Girl about the micropost’s associated user just by including a user in the definition of the factory:

	factory :micropost do
	  content "Lorem ipsum"
	  user
	end

As we’ll see in the next section, this allows us to define factory microposts as follows:

	FactoryGirl.create(:micropost, user: @user, created_at: 1.day.ago)

### Default scope

By default, using user.microposts to pull a user’s microposts from the database makes no guarantees about the order of the posts, but (following the convention of blogs and Twitter) we want the microposts to come out in reverse order of when they were created, i.e., most recent first. To test this ordering, we first create a couple of microposts as follows:

	FactoryGirl.create(:micropost, user: @user, created_at: 1.day.ago)
	FactoryGirl.create(:micropost, user: @user, created_at: 1.hour.ago)

Here we indicate (using the time helpers discussed in Box 8.1) that the second post was created more recently, i.e., **1.hour.ago**, while the first post was created **1.day.ago**. Note how convenient the use of Factory Girl is: we can set `created_at` manually, which Active Record won’t allow us to do. (Recall that `created_at` and `updated_at` are “magic” columns, automatically set to the proper creation and update timestamps, so any explicit initialization values are overwritten by the magic.)

Most database adapters (including the one for SQLite) return the microposts in order of their ids, so we can arrange for an initial test that almost certainly fails using the code in Listing 10.10. This uses the **let!** (read “let bang”) method in place of let; the reason is that let variables are **lazy**, meaning that *they only spring into existence when referenced*. The problem is that we want the microposts to exist immediately, so that the timestamps are in the right order and so that @user.microposts isn’t empty. We accomplish this with let!, which forces the corresponding variable to come into existence immediately.

	Listing 10.10: Testing the order of a user’s microposts.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do
	  .
	  .
	  .
	  describe "micropost associations" do

	    before { @user.save }
	    let!(:older_micropost) do
	      FactoryGirl.create(:micropost, user: @user, created_at: 1.day.ago)
	    end
	    let!(:newer_micropost) do
	      FactoryGirl.create(:micropost, user: @user, created_at: 1.hour.ago)
	    end

	    it "should have the right microposts in the right order" do
	      expect(@user.microposts.to_a).to eq [newer_micropost, older_micropost]
	    end
	  end
	end

The key line here is

	expect(@user.microposts.to_a).to eq [newer_micropost, older_micropost]

indicating that the posts should be ordered newest first. This should fail because by default the posts will be ordered by id, i.e., `[older_micropost, newer_micropost]`. This test also verifies the basic correctness of the `has_many` association itself, by checking (as indicated in Table 10.1) that user.microposts effectively returns an array of microposts. The **to_a** method, discussed before in Section 4.3.1, converts @user.microposts from its default state (which happens to be an Active Record “collection proxy”) to a proper array appropriate for comparison with the one we constructed by hand.

To get the ordering test to pass, we use a Rails facility called **default_scope** with an order argument, as shown in Listing 10.11. (This is our first example of the notion of scope. We will learn about scope in a more general context in Chapter 11.)

	Listing 10.11: Ordering the microposts with default_scope.
	app/models/micropost.rb
	 class Micropost < ActiveRecord::Base
	  belongs_to :user
	  default_scope -> { order('created_at DESC') }
	  validates :user_id, presence: true
	end

The order here is **’created_at DESC’**, where DESC is SQL for **“descending”**, i.e., in descending order from newest to oldest.

As of Rails 4.0, all scopes take an **anonymous function** that returns the criteria desired for the scope, mainly so that the scope need not be evaluated immediately, but rather can be loaded later on an as-needed basis (so-called lazy evaluation). In the present case, this function is

	-> { order('created_at DESC') }

The syntax for this kind of object, called a **Proc** (procedure) or **lambda**, is the arrow `->`. It takes in a block (Section 4.3.2) and then evaluates it when called with the call method. We can see how it works at the console:

	>> -> { puts "foo" }
	=> #<Proc:0x007fab938d0108@(irb):1 (lambda)>
	>> -> { puts "foo" }.call
	foo
	=> nil

(Procs are a somewhat advanced Ruby topic, so don’t worry if they don’t make sense right away.)

### Dependent: destroy
Apart from proper ordering, there is a second refinement we’d like to add to microposts. Recall from Section 9.4 that site administrators have the power to destroy users. It stands to reason that, if a user is destroyed, the user’s microposts should be destroyed as well. We can test for this by first destroying a micropost’s user and then verifying that the associated microposts are no longer in the database.

In order to test destroying microposts properly, we first need to capture a given user’s posts in a local variable, and then destroy the user. A straighforward implementation looks like this:

	microposts = @user.microposts.to_a
	@user.destroy
	expect(microposts).not_to be_empty
	microposts.each do |micropost|
	  # Make sure the micropost doesn't appear in the database.
	end

Here the call to **to_a** effectively makes a copy of the microposts, and we’ve included the line

	expect(microposts).not_to be_empty

as a safety check to catch any errors should the `to_a` ever be accidentally removed. The issue is that, without `to_a`, destroying the user would destroy the posts in the microposts variable, and as a result

We can express the expectation that the microposts don’t appear in the database as follows:

	microposts.each do |micropost|
	  expect(Micropost.where(id: micropost.id)).to be_empty
	end

Here we have used **Micropost.where** instead of **Micropost.find** because it returns an empty object if the record is not found instead of raising an exception, which is a little easier to test. (In case you’re curious, the code

	expect do
	  Micropost.find(micropost)
	end.to raise_error(ActiveRecord::RecordNotFound)

does the trick in this case.)

Putting everything together leads to the code in Listing 10.12.

	Listing 10.12: Testing that microposts are destroyed when users are.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do
	  .
	  .
	  .
	  describe "micropost associations" do

	    before { @user.save }
	    let!(:older_micropost) do
	      FactoryGirl.create(:micropost, user: @user, created_at: 1.day.ago)
	    end
	    let!(:newer_micropost) do
	      FactoryGirl.create(:micropost, user: @user, created_at: 1.hour.ago)
	    end
	    .
	    .
	    .
	    it "should destroy associated microposts" do
	      microposts = @user.microposts.to_a
	      @user.destroy
	      expect(microposts).not_to be_empty
	      microposts.each do |micropost|
	        expect(Micropost.where(id: micropost.id)).to be_empty
	      end
	    end
	  end
	end

The application code to get Listing 10.12 to pass is less than one line; in fact, it’s just an option to the has_many association method, as shown in Listing 10.13.

	Listing 10.13: Ensuring that a user’s microposts are destroyed along with the user.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  has_many :microposts, dependent: :destroy
	  .
	  .
	  .
	end

With that, the final form of the user/micropost association is in place, and all the tests should be passing:

	$ bundle exec rspec spec/

## 10.1.5 - Content validations
Before leaving the Micropost model, we’ll add validations for the micropost content (following the example from Section 2.3.2). Like the **user_id**, the **content** attribute must be present, and it is further constrained to be no longer than 140 characters, making it an honest micropost. The tests generally follow the examples from the User model validation tests in Section 6.2, as shown in Listing 10.14.

	Listing 10.14: Tests for the Micropost model validations.
	spec/models/micropost_spec.rb
	 require 'spec_helper'

	describe Micropost do

	  let(:user) { FactoryGirl.create(:user) }
	  before { @micropost = user.microposts.build(content: "Lorem ipsum") }
	  .
	  .
	  .
	  describe "when user_id is not present" do
	    before { @micropost.user_id = nil }
	    it { should_not be_valid }
	  end

	  describe "with blank content" do
	    before { @micropost.content = " " }
	    it { should_not be_valid }
	  end

	  describe "with content that is too long" do
	    before { @micropost.content = "a" * 141 }
	    it { should_not be_valid }
	  end
	end

The application code is a one-liner:

	validates :content, presence: true, length: { maximum: 140 }

The resulting Micropost model is shown in Listing 10.15.

	Listing 10.15: The Micropost model validations.
	app/models/micropost.rb
	 class Micropost < ActiveRecord::Base
	  belongs_to :user
	  default_scope -> { order('created_at DESC') }
	  validates :content, presence: true, length: { maximum: 140 }
	  validates :user_id, presence: true
	end

# 10.2 - Showing microposts
Although we don’t yet have a way to create microposts through the web—that comes in Section 10.3.2—that won’t stop us from displaying them (and testing that display). Following Twitter’s lead, we’ll plan to display a user’s microposts not on a separate microposts index page, but rather directly on the user show page itself, as mocked up in Figure 10.4. We’ll start with fairly simple ERb templates for adding a micropost display to the user profile, and then we’ll add microposts to the sample data populator from Section 9.3.2 so that we have something to display.

<figure>
  <figcaption style="text-align:center;">Figure 10.4: A mockup of a profile page with microposts.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/user_microposts_mockup_bootstrap.png" alt="profile page with microposts" title="profile page with microposts">
</figure>

## 10.2.1 - Augmenting the user show page
We begin with tests for displaying the user’s microposts, which we’ll create in the request spec for Users. Our strategy is to create a couple of factory microposts associated with the user, and then verify that the show page contains each post’s content. We’ll also verify that, as in Figure 10.4, the total number of microposts also gets displayed.

We can create the posts with the let method, but as in Listing 10.10 we want the association to exist immediately so that the posts appear on the user show page. To accomplish this, we use the **let!** variant:

	let(:user) { FactoryGirl.create(:user) }
	let!(:m1) { FactoryGirl.create(:micropost, user: user, content: "Foo") }
	let!(:m2) { FactoryGirl.create(:micropost, user: user, content: "Bar") }

	before { visit user_path(user) }

With the microposts so defined, we can test for their appearance on the profile page using the code in Listing 10.16.

	Listing 10.16: A test for showing microposts on the user show page.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do
	  .
	  .
	  .
	  describe "profile page" do
	    let(:user) { FactoryGirl.create(:user) }
	    let!(:m1) { FactoryGirl.create(:micropost, user: user, content: "Foo") }
	    let!(:m2) { FactoryGirl.create(:micropost, user: user, content: "Bar") }

	    before { visit user_path(user) }

	    it { should have_content(user.name) }
	    it { should have_title(user.name) }

	    describe "microposts" do
	      it { should have_content(m1.content) }
	      it { should have_content(m2.content) }
	      it { should have_content(user.microposts.count) }
	    end
	  end
	  .
	  .
	  .
	end

Note here that we can use the **count** method through the association:

	user.microposts.count

The association count method is smart, and performs the *count directly in the database*. In particular, it does not pull all the microposts out of the database and then call length on the resulting array, as this could become inefficient as the number of microposts grew. Instead, *it asks the database to count the microposts with the given user_id*. In the unlikely event that finding the count is still a bottleneck in your application, you can make it even faster with a [counter cache](http://railscasts.com/episodes/23-counter-cache-column).

We’ll get started on the application code by inserting a list of microposts into the user profile page, as shown in Listing 10.17.

	Listing 10.17: Adding microposts to the user show page.
	app/views/users/show.html.erb
	 <% provide(:title, @user.name) %>
	<div class="row">
	  .
	  .
	  .
	  <aside>
	    .
	    .
	    .
	  </aside>
	  <div class="span8">
	    <% if @user.microposts.any? %>
	      <h3>Microposts (<%= @user.microposts.count %>)</h3>
	      <ol class="microposts">
	        <%= render @microposts %>
	      </ol>
	      <%= will_paginate @microposts %>
	    <% end %>
	  </div>
	</div>

We’ll deal with the microposts list momentarily, but there are several other things to note first. In Listing 10.17, the use of if @**user.microposts.any?** (a construction we saw before in Listing 7.24) makes sure that an empty list won’t be displayed when the user has no microposts.

Also note from Listing 10.17 that we’ve preemptively added pagination for microposts through

	<%= will_paginate @microposts %>

If you compare this with the analogous line on the user index page, Listing 9.33, you’ll see that before we had just

	<%= will_paginate %>

This worked because, in the context of the Users controller, `will_paginate` assumes the existence of an instance variable called @users (which, as we saw in Section 9.3.3, should be of class ActiveRecord::Relation). In the present case, since *we are still in the Users controller but want to paginate microposts instead*, we pass an explicit @microposts variable to will_paginate. Of course, this means that we will have to define such a variable in the user show action (Listing 10.19).

Finally, note that we have taken this opportunity to add a count of the current number of microposts:

	<h3>Microposts (<%= @user.microposts.count %>)</h3>

As noted, **@user.microposts.count** is the analogue of the User.count method, except that it counts the microposts belonging to a given user through the **user/micropost** association.

We come finally to the micropost list itself:

	<ol class="microposts">
	  <%= render @microposts %>
	</ol>

This code, which uses the ordered list tag **ol**, is responsible for generating the list of microposts, but you can see that it just defers the heavy lifting to a micropost partial. We saw in Section 9.3.4 that the code

	<%= render @users %>

automatically renders each of the users in the @users variable using the _user.html.erb partial. Similarly, the code

	<%= render @microposts %>

does exactly the same thing for microposts. This means that we must define a _micropost.html.erb partial (along with a micropost views directory), as shown in Listing 10.18.

	Listing 10.18: A partial for showing a single micropost.
	app/views/microposts/_micropost.html.erb
	 <li>
	  <span class="content"><%= micropost.content %></span>
	  <span class="timestamp">
	    Posted <%= time_ago_in_words(micropost.created_at) %> ago.
	  </span>
	</li>

This uses the awesome **time_ago_in_words** helper method, whose effect we will see in Section 10.2.2.

Thus far, despite defining all the relevant ERb templates, the test in Listing 10.16 should have been failing for want of an @microposts variable. We can get it to pass with Listing 10.19.

	Listing 10.19: Adding an @microposts instance variable to the user show action.
	app/controllers/users_controller.rb
	 class UsersController < ApplicationController
	  .
	  .
	  .
	  def show
	    @user = User.find(params[:id])
	    @microposts = @user.microposts.paginate(page: params[:page])
	  end
	  .
	  .
	  .
	end

Notice here how clever paginate is—it even works through the microposts association, reaching into the microposts table and pulling out the desired page of microposts.

## 10.2.2 - Sample microposts
Adding sample microposts for all the users actually takes a rather long time, so first we’ll select just the first six users using the **:limit** option to the **User.all** method:

	users = User.all(limit: 6)

We then make 50 microposts for each user (plenty to overflow the pagination limit of 30), generating sample content for each micropost using the Faker gem’s handy [Lorem.sentence](http://rubydoc.info/gems/faker/1.3.0/Faker/Lorem) method. (Faker::Lorem.sentence returns lorem ipsum text; as noted in Chapter 6, lorem ipsum has a fascinating back story.) The result is the new sample data populator shown in Listing 10.20.

	Listing 10.20: Adding microposts to the sample data.
	lib/tasks/sample_data.rake
	 namespace :db do
	  desc "Fill database with sample data"
	  task populate: :environment do
	    .
	    .
	    .
	    users = User.all(limit: 6)
	    50.times do
	      content = Faker::Lorem.sentence(5)
	      users.each { |user| user.microposts.create!(content: content) }
	    end
	  end
	end

Of course, to generate the new sample data we have to run the db:populate Rake task:

	$ bundle exec rake db:reset
	$ bundle exec rake db:populate
	$ bundle exec rake test:prepare

With that, we are in a position to enjoy the fruits of our Section 10.2.1 labors by displaying information for each micropost

The page shown in Figure 10.6 has no micropost-specific styling, so let’s add some (Listing 10.21) and take a look the resulting pages.Figure 10.7, which displays the user profile page for the first (signed-in) user, while Figure 10.8 shows the profile for a second user. Finally, Figure 10.9 shows the second page of microposts for the first user, along with the pagination links at the bottom of the display. In all three cases, observe that each micropost display indicates the time since it was created (e.g., “Posted 1 minute ago.”); this is the work of the **time_ago_in_words** method from Listing 10.18. If you wait a couple minutes and reload the pages, you’ll see how the text gets automatically updated based on the new time.

	Listing 10.21: The CSS for microposts (including all the CSS for this chapter).
	app/assets/stylesheets/custom.css.scss
	 .
	.
	.
	/* microposts */

	.microposts {
	  list-style: none;
	  margin: 10px 0 0 0;

	  li {
	    padding: 10px 0;
	    border-top: 1px solid #e8e8e8;
	  }
	}
	.content {
	  display: block;
	}
	.timestamp {
	  color: $grayLight;
	}
	.gravatar {
	  float: left;
	  margin-right: 10px;
	}
	aside {
	  textarea {
	    height: 100px;
	    margin-bottom: 5px;
	  }
	}

# 10.3 - Manipulating microposts
Having finished both the data modeling and display templates for microposts, we now turn our attention to the interface for creating them through the web. The result will be our third example of using an HTML form to create a resource—in this case, a Microposts resource. In this section, we’ll also see the first hint of a **status feed**—a notion brought to full fruition in Chapter 11. Finally, as with users, we’ll make it possible to destroy microposts through the web.

There is one break with past convention worth noting: the interface to the Microposts resource will run principally through the **Users** and **StaticPages** controllers, so we won’t need actions like **new** or **edit** in the Microposts controller; we’ll only need **create** and **destroy**. This means that the routes for the Microposts resource are unusually simple, as seen in Listing 10.22. The code in Listing 10.22 leads in turn to the RESTful routes shown in Table 10.2, which is a small subset of the full set of routes seen in Table 2.3. Of course, this simplicity is a sign of being more advanced, not less—we’ve come a long way since our reliance on scaffolding in Chapter 2, and we no longer need most of its complexity.

	Listing 10.22: Routes for the Microposts resource.
	config/routes.rb
	 SampleApp::Application.routes.draw do
	  resources :users
	  resources :sessions,   only: [:new, :create, :destroy]
	  resources :microposts, only: [:create, :destroy]
	  .
	  .
	  .
	end

HTTP request |	URL |	Action |	Purpose
-|-|-|-
POST	| /microposts |	create |	create a new micropost
DELETE	| /microposts/1 |	destroy	| delete micropost with id 1

## 10.3.1 - Access control
We begin our development of the Microposts resource with some **access control** in the Microposts controller. The idea is simple: both the create and destroy actions should require users to be signed in. The RSpec code to test for this appears in Listing 10.23. (We’ll test for and add a third protection—ensuring that only a micropost’s user can destroy it—in Section 10.3.4.)

	Listing 10.23: Access control tests for microposts.
	spec/requests/authentication_pages_spec.rb
	 require 'spec_helper'

	describe "Authentication" do
	  .
	  .
	  .
	  describe "authorization" do

	    describe "for non-signed-in users" do
	      let(:user) { FactoryGirl.create(:user) }
	      .
	      .
	      .
	      describe "in the Microposts controller" do

	        describe "submitting to the create action" do
	          before { post microposts_path }
	          specify { expect(response).to redirect_to(signin_path) }
	        end

	        describe "submitting to the destroy action" do
	          before { delete micropost_path(FactoryGirl.create(:micropost)) }
	          specify { expect(response).to redirect_to(signin_path) }
	        end
	      end
	      .
	      .
	      .
	    end
	  end
	end

Rather than using the (yet-to-be-built) web interface for microposts, the code in Listing 10.23 operates at the level of the individual micropost actions, a strategy we first saw in Listing 9.13. In this case, a non-signed-in user is redirected upon submitting a POST request to **/microposts** (`post microposts_path`, which hits the create action) or submitting a DELETE request to /microposts/1 (`delete micropost_path(micropost)`, which hits the destroy action).

Writing the application code needed to get the tests in Listing 10.23 to pass requires a little refactoring first. Recall from Section 9.2.1 that we enforced the signin requirement using a before filter that called the **signed_in_user** method (Listing 9.12). At the time, we only needed that method in the Users controller, but now we find that we need it in the Microposts controller as well, so we’ll move it into the Sessions helper, as shown in Listing 10.24.8

	Listing 10.24: Moving the signed_in_user method into the Sessions helper.
	app/helpers/sessions_helper.rb
	 module SessionsHelper
	  .
	  .
	  .
	  def current_user?(user)
	    user == current_user
	  end

	  def signed_in_user
	    unless signed_in?
	      store_location
	      redirect_to signin_url, notice: "Please sign in."
	    end
	  end
	  .
	  .
	  .
	end

To avoid code repetition, you should also remove **signed_in_user** from the Users controller at this time.

With the code in Listing 10.24, the **signed_in_user** method is now available in the Microposts controller, which means that we can restrict access to the create and destroy actions with the before filter shown in Listing 10.25. (Since we didn’t generate it at the command line, you will have to create the Microposts controller file by hand.)

	Listing 10.25: Adding authentication to the Microposts controller actions.
	app/controllers/microposts_controller.rb
	 class MicropostsController < ApplicationController
	  before_action :signed_in_user

	  def create
	  end

	  def destroy
	  end
	end

Note that we haven’t restricted the actions the before filter applies to since it applies to them both by default. If we were to add, say, an index action accessible even to non-signed-in users, we would need to specify the protected actions explicitly:

	class MicropostsController < ApplicationController
	  before_action :signed_in_user, only: [:create, :destroy]

	  def index
	  end

	  def create
	  end

	  def destroy
	  end
	end

At this point, the tests should pass:

	$ bundle exec rspec spec/requests/authentication_pages_spec.rb

## 10.3.2 - Creating microposts
In Chapter 7, we implemented user signup by making an HTML form that issued an HTTP POST request to the create action in the Users controller. The implementation of micropost creation is similar; the main difference is that, rather than using a separate page at **/microposts/new**, we will (following Twitter’s convention) put the form on the Home page itself (i.e., the root path /), as mocked up in Figure 10.10.

<figure>
  <figcaption style="text-align:center;">Figure 10.10: A mockup of the Home page with a form for creating microposts.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/home_page_with_micropost_form_mockup_bootstrap.png" alt="homepage with mircropost" title="homepage with mircropost">
</figure>

When we last left the Home page, it appeared as in Figure 5.6—that is, it had a “Sign up now!” button in the middle. Since a micropost creation form only makes sense in the context of a particular signed-in user, one goal of this section will be to **serve different versions of the Home page depending on a visitor’s signin status**. We’ll implement this in Listing 10.28 below, but we can still write the tests now. As with the Users resource, we’ll use an integration test:

	$ rails generate integration_test micropost_pages

The micropost creation tests then parallel those for user creation from Listing 7.16; the result appears in Listing 10.26.

	Listing 10.26: Tests for creating microposts.
	spec/requests/micropost_pages_spec.rb
	 require 'spec_helper'

	describe "Micropost pages" do

	  subject { page }

	  let(:user) { FactoryGirl.create(:user) }
	  before { sign_in user }

	  describe "micropost creation" do
	    before { visit root_path }

	    describe "with invalid information" do

	      it "should not create a micropost" do
	        expect { click_button "Post" }.not_to change(Micropost, :count)
	      end

	      describe "error messages" do
	        before { click_button "Post" }
	        it { should have_content('error') }
	      end
	    end

	    describe "with valid information" do

	      before { fill_in 'micropost_content', with: "Lorem ipsum" }
	      it "should create a micropost" do
	        expect { click_button "Post" }.to change(Micropost, :count).by(1)
	      end
	    end
	  end
	end

We’ll start with the create action for microposts, which is similar to its user analogue (Listing 7.26); the principal difference lies in using the **user/**micropost association to build the new micropost, as seen in Listing 10.27. Note the use of strong parameters via micropost_params, which permits only the micropost content to be edited through the web.

	Listing 10.27: The Microposts controller create action.
	app/controllers/microposts_controller.rb
	 class MicropostsController < ApplicationController
	  before_action :signed_in_user

	  def create
	    @micropost = current_user.microposts.build(micropost_params)
	    if @micropost.save
	      flash[:success] = "Micropost created!"
	      redirect_to root_url
	    else
	      render 'static_pages/home'
	    end
	  end

	  def destroy
	  end

	  private

	    def micropost_params
	      params.require(:micropost).permit(:content)
	    end
	end

To build a form for creating microposts, we use the code in Listing 10.28, which serves up different HTML based on whether the site visitor is signed in or not.

	Listing 10.28: Adding microposts creation to the Home page (/).
	app/views/static_pages/home.html.erb
	 <% if signed_in? %>
	  <div class="row">
	    <aside class="span4">
	      <section>
	        <%= render 'shared/user_info' %>
	      </section>
	      <section>
	        <%= render 'shared/micropost_form' %>
	      </section>
	    </aside>
	  </div>
	<% else %>
	  <div class="center hero-unit">
	    <h1>Welcome to the Sample App</h1>

	    <h2>
	      This is the home page for the
	      <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	      sample application.
	    </h2>

	    <%= link_to "Sign up now!", signup_path,
	                                class: "btn btn-large btn-primary" %>
	  </div>

	  <%= link_to image_tag("rails.png", alt: "Rails"), 'http://rubyonrails.org/' %>
	<% end %>

Having so much code in each branch of the if-else conditional is a bit messy, and cleaning it up using partials is left as an exercise (Section 10.5). Filling in the necessary partials from Listing 10.28 isn’t an exercise, though; we fill in the new Home page sidebar in Listing 10.29 and the micropost form partial in Listing 10.30.

	Listing 10.29: The partial for the user info sidebar.
	app/views/shared/_user_info.html.erb
	 <%= link_to gravatar_for(current_user, size: 52), current_user %>
	<h1>
	  <%= current_user.name %>
	</h1>
	<span>
	  <%= link_to "view my profile", current_user %>
	</span>
	<span>
	  <%= pluralize(current_user.microposts.count, "micropost") %>
	</span>

As in Listing 9.24, the code in Listing 10.29 uses the version of the gravatar_for helper defined in Listing 7.30.

Note that, as in the profile sidebar (Listing 10.17), the user info in Listing 10.29 displays the total number of microposts for the user. There’s a slight difference in the display, though; in the profile sidebar, “Microposts” is a label, and showing “Microposts (1)” makes sense. In the present case, though, saying “1 microposts” is ungrammatical, so we arrange to display “1 micropost” (but “2 microposts”) using **pluralize**.

We next define the form for creating microposts (Listing 10.30), which is similar to the signup form in Listing 7.17.

	Listing 10.30: The form partial for creating microposts.
	app/views/shared/_micropost_form.html.erb
	 <%= form_for(@micropost) do |f| %>
	  <%= render 'shared/error_messages', object: f.object %>
	  <div class="field">
	    <%= f.text_area :content, placeholder: "Compose new micropost..." %>
	  </div>
	  <%= f.submit "Post", class: "btn btn-large btn-primary" %>
	<% end %>

We need to make two changes before the form in Listing 10.30 will work. First, we need to define @micropost, which (as before) we do through the association:

	@micropost = current_user.microposts.build

The result appears in Listing 10.31.

	Listing 10.31: Adding a micropost instance variable to the home action.
	app/controllers/static_pages_controller.rb
	 class StaticPagesController < ApplicationController

	  def home
	    @micropost = current_user.microposts.build if signed_in?
	  end
	  .
	  .
	  .
	end

The code in Listing 10.31 has the advantage that it will break the test suite if we forget to require the user to sign in.

The second change needed to get Listing 10.30 to work is to redefine the error messages partial so that

	<%= render 'shared/error_messages', object: f.object %>

works. You may recall from Listing 7.23 that the error messages partial references the @user variable explicitly, but in the present case we have an @micropost variable instead. We should define an error messages partial that works regardless of the kind of object passed to it. Happily, the form variable f can access the associated object through f.object, so that in

	form_for(@user) do |f|

f.object is @user, and in

	form_for(@micropost) do |f|

f.object is @micropost.

To pass the object to the partial, we use a hash with value equal to the object and key equal to the desired name of the variable in the partial, which is what this code accomplishes:

	<%= render 'shared/error_messages', object: f.object %>

In other words, object: **f.object** creates a variable called object in the error_messages partial. We can use this object to construct a customized error message, as shown in Listing 10.32.

	Listing 10.32: Updating the error-messages partial from Listing 7.24 to work with other objects.
	app/views/shared/_error_messages.html.erb
	 <% if object.errors.any? %>
	  <div id="error_explanation">
	    <div class="alert alert-error">
	      The form contains <%= pluralize(object.errors.count, "error") %>.
	    </div>
	    <ul>
	    <% object.errors.full_messages.each do |msg| %>
	      <li>* <%= msg %></li>
	    <% end %>
	    </ul>
	  </div>
	<% end %>

As this point, the tests in Listing 10.26 should be passing:

	$ bundle exec rspec spec/requests/micropost_pages_spec.rb

Unfortunately, the User request spec is now broken because the signup and edit forms use the old version of the error messages partial. To fix them, we’ll update them with the more general version, as shown in Listing 10.33 and Listing 10.34. (Note: Your code will differ if you implemented Listing 9.49 and Listing 9.50 from the exercises in Section 9.6. [Mutatis mutandis](http://en.wikipedia.org/wiki/Mutatis_mutandis).)

	Listing 10.33: Updating the rendering of user signup errors.
	app/views/users/new.html.erb
	 <% provide(:title, 'Sign up') %>
	<h1>Sign up</h1>

	<div class="row">
	  <div class="span6 offset3">
	    <%= form_for(@user) do |f| %>
	      <%= render 'shared/error_messages', object: f.object %>
	      .
	      .
	      .
	    <% end %>
	  </div>
	</div>

	Listing 10.34: Updating the errors for editing users.
	app/views/users/edit.html.erb
	 <% provide(:title, "Edit user") %>
	<h1>Update your profile</h1>

	<div class="row">
	  <div class="span6 offset3">
	    <%= form_for(@user) do |f| %>
	      <%= render 'shared/error_messages', object: f.object %>
	      .
	      .
	      .
	    <% end %>

	    <%= gravatar_for(@user) %>
	    <a href="http://gravatar.com/emails">change</a>
	  </div>
	</div>

At this point, all the tests should be passing:

	$ bundle exec rspec spec/

## 10.3.3 - A proto-feed
The comment at the end of Section 10.3.2 *alluded to a problem*: the current Home page doesn’t display any microposts. If you like, you can verify that the form shown in Figure 10.11 is working by submitting a valid entry and then navigating to the profile page to see the post, but that’s rather cumbersome. It would be far better to *have a feed of microposts that includes the user’s own posts*, as mocked up in Figure 10.13. (*In Chapter 11, we’ll generalize this feed to include the microposts of users being followed by the current user*.)

<figure>
  <figcaption style="text-align:center;">Figure 10.13: A mockup of the Home page with a proto-feed.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/proto_feed_mockup_bootstrap.png" alt="feed" title="feed">
</figure>

Since each user should have a feed, we are led naturally to a **feed** method in the User model. Eventually, we will test that the feed returns the microposts of the users being followed, but for now we’ll just test that the feed method includes the current user’s microposts but excludes the posts of a different user. We can express these requirements in code with Listing 10.35.

	Listing 10.35: Tests for the (proto-)status feed.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do
	  .
	  .
	  .
	  it { should respond_to(:microposts) }
	  it { should respond_to(:feed) }
	  .
	  .
	  .
	  describe "micropost associations" do

	    before { @user.save }
	    let!(:older_micropost) do
	      FactoryGirl.create(:micropost, user: @user, created_at: 1.day.ago)
	    end
	    let!(:newer_micropost) do
	      FactoryGirl.create(:micropost, user: @user, created_at: 1.hour.ago)
	    end
	    .
	    .
	    .
	    describe "status" do
	      let(:unfollowed_post) do
	        FactoryGirl.create(:micropost, user: FactoryGirl.create(:user))
	      end

	      its(:feed) { should include(newer_micropost) }
	      its(:feed) { should include(older_micropost) }
	      its(:feed) { should_not include(unfollowed_post) }
	    end
	  end
	end

These tests introduce (via the RSpec boolean convention) the array **include?** method, which simply checks if an array includes the given element:

	$ rails console
	>> a = [1, "foo", :bar]
	>> a.include?("foo")
	=> true
	>> a.include?(:bar)
	=> true
	>> a.include?("baz")
	=> false

This example shows just how flexible the RSpec boolean convention is; even though include is already a Ruby keyword (used to include a module, as seen in, e.g., Listing 8.14), in this context RSpec correctly guesses that we want to test array inclusion.

We can arrange for an appropriate micropost feed method by selecting all the microposts with user_id equal to the current user’s id, which we accomplish using the **where** method on the Micropost model, as shown in Listing 10.36.

	Listing 10.36: A preliminary implementation for the micropost status feed.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  .
	  .
	  .
	  def feed
	    # This is preliminary. See "Following users" for the full implementation.
	    Micropost.where("user_id = ?", id)
	  end
	  .
	  .
	  .
	end

The question mark in

	Micropost.where("user_id = ?", id)

ensures that id is properly escaped before being included in the underlying SQL query, thereby avoiding a serious security hole called **SQL injection**. The id attribute here is just an integer (i.e., self.id, the unique ID of the user), so there is no danger in this case, but always escaping variables injected into SQL statements is a good habit to cultivate.

Alert readers might note at this point that the code in Listing 10.36 is essentially equivalent to writing

	def feed
	  microposts
	end

We’ve used the code in Listing 10.36 instead because it generalizes much more naturally to the full status feed needed in Chapter 11.

To test the display of the status feed, we first create a couple of microposts and then verify that a list element (li) appears on the page for each one (Listing 10.37).

	Listing 10.37: A test for rendering the feed on the Home page.
	spec/requests/static_pages_spec.rb
	 require 'spec_helper'

	describe "Static pages" do

	  subject { page }

	  describe "Home page" do
	    .
	    .
	    .
	    describe "for signed-in users" do
	      let(:user) { FactoryGirl.create(:user) }
	      before do
	        FactoryGirl.create(:micropost, user: user, content: "Lorem ipsum")
	        FactoryGirl.create(:micropost, user: user, content: "Dolor sit amet")
	        sign_in user
	        visit root_path
	      end

	      it "should render the user's feed" do
	        user.feed.each do |item|
	          expect(page).to have_selector("li##{item.id}", text: item.content)
	        end
	      end
	    end
	  end
	  .
	  .
	  .
	end

Listing 10.37 assumes that each feed item has a unique CSS id, so that

	expect(page).to have_selector("li##{item.id}", text: item.content)

will generate a match for each item. (Note that the first `#` in `li##{item.id}` is Capybara syntax for a CSS id, whereas the second `#` is the beginning of a Ruby *string interpolation* `#{}`.)

To use the feed in the sample application, we add an **@feed_items** instance variable for the current user’s (paginated) feed, as in Listing 10.38, and then add a feed partial (Listing 10.39) to the Home page (Listing 10.41). (Adding tests for pagination is left as an exercise; see Section 10.5.)

	Listing 10.38: Adding a feed instance variable to the home action.
	app/controllers/static_pages_controller.rb
	 class StaticPagesController < ApplicationController

	  def home
	    if signed_in?
	      @micropost  = current_user.microposts.build
	      @feed_items = current_user.feed.paginate(page: params[:page])
	    end
	  end
	  .
	  .
	  .
	end

	Listing 10.39: The status feed partial.
	app/views/shared/_feed.html.erb
	 <% if @feed_items.any? %>
	  <ol class="microposts">
	    <%= render partial: 'shared/feed_item', collection: @feed_items %>
	  </ol>
	  <%= will_paginate @feed_items %>
	<% end %>

The status feed partial defers the feed item rendering to a feed item partial using the code

	<%= render partial: 'shared/feed_item', collection: @feed_items %>

Here we pass a **:collection** parameter with the feed items, which causes render to use the given partial (’feed_item’ in this case) to render each item in the collection. (We have omitted the :partial parameter in previous renderings, writing, e.g., render ’shared/micropost’, but with a :collection parameter that syntax doesn’t work.) The feed item partial itself appears in Listing 10.40.

	Listing 10.40: A partial for a single feed item.
	app/views/shared/_feed_item.html.erb
	 <li id="<%= feed_item.id %>">
	  <%= link_to gravatar_for(feed_item.user), feed_item.user %>
	  <span class="user">
	    <%= link_to feed_item.user.name, feed_item.user %>
	  </span>
	  <span class="content"><%= feed_item.content %></span>
	  <span class="timestamp">
	    Posted <%= time_ago_in_words(feed_item.created_at) %> ago.
	  </span>
	</li>

Listing 10.40 also adds a CSS id for each feed item using

	<li id="<%= feed_item.id %>">

as required by the test in Listing 10.37.

We can then add the feed to the Home page by rendering the feed partial as usual (Listing 10.41). The result is a display of the feed on the Home page, as required (Figure 10.14).

	Listing 10.41: Adding a status feed to the Home page.
	app/views/static_pages/home.html.erb
	 <% if signed_in? %>
	  <div class="row">
	    .
	    .
	    .
	    <div class="span8">
	      <h3>Micropost Feed</h3>
	      <%= render 'shared/feed' %>
	    </div>
	  </div>
	<% else %>
	  .
	  .
	  .
	<% end %>

<figure>
  <figcaption style="text-align:center;">Figure 10.14: The Home page (/) with a proto-feed.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/home_with_proto_feed_bootstrap.png" alt="feed" title="feed">
</figure>

At this point, creating a new micropost works as expected, as seen in Figure 10.15. There is one *subtlety*, though: on failed micropost submission, the Home page expects an **@feed_items** instance variable, so failed submissions currently break (as you should be able to verify by running your test suite). The easiest solution is to suppress the feed entirely by assigning it an empty array, as shown in Listing 10.42


<figure>
  <figcaption style="text-align:center;">Figure 10.15: The Home page after creating a new micropost.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/micropost_created_bootstrap.png" alt="feed" title="feed">
</figure>

	Listing 10.42: Adding an (empty) @feed_items instance variable to the create action.
	app/controllers/microposts_controller.rb
	 class MicropostsController < ApplicationController
	  .
	  .
	  .
	  def create
	    @micropost = current_user.microposts.build(micropost_params)
	    if @micropost.save
	      flash[:success] = "Micropost created!"
	      redirect_to root_url
	    else
	      @feed_items = []
	      render 'static_pages/home'
	    end
	  end
	  .
	  .
	  .
	end

At this point, the proto-feed should be working, and the test suite should pass:

	$ bundle exec rspec spec/

## 10.3.4 - Destroying microposts
The last piece of functionality to add to the Microposts resource is the ability to destroy posts. As with user deletion (Section 9.4.2), we accomplish this with **“delete”** links, as mocked up in Figure 10.16. Unlike that case, which restricted user destruction to admin users, the delete links will work only for microposts created by the current user.

Our first step is to add a delete link to the micropost partial as in Listing 10.40, and while we’re at it we’ll add a similar link to the feed item partial from Listing 10.40. The results appear in Listing 10.43 and Listing 10.44. (The two cases are almost identical, and eliminating this duplication is left as an exercise (Section 10.5).)

	Listing 10.43: Adding a delete link to the micropost partial.
	app/views/microposts/_micropost.html.erb
	 <li>
	  <span class="content"><%= micropost.content %></span>
	  <span class="timestamp">
	    Posted <%= time_ago_in_words(micropost.created_at) %> ago.
	  </span>
	  <% if current_user?(micropost.user) %>
	    <%= link_to "delete", micropost, method: :delete,
	                                     data: { confirm: "You sure?" },
	                                     title: micropost.content %>
	  <% end %>
	</li>

	Listing 10.44: The feed item partial with added delete link.
	app/views/shared/_feed_item.html.erb
	 <li id="<%= feed_item.id %>">
	  <%= link_to gravatar_for(feed_item.user), feed_item.user %>
	    <span class="user">
	      <%= link_to feed_item.user.name, feed_item.user %>
	    </span>
	    <span class="content"><%= feed_item.content %></span>
	    <span class="timestamp">
	      Posted <%= time_ago_in_words(feed_item.created_at) %> ago.
	    </span>
	  <% if current_user?(feed_item.user) %>
	    <%= link_to "delete", feed_item, method: :delete,
	                                     data: { confirm: "You sure?" },
	                                     title: feed_item.content %>
	  <% end %>
	</li>

The test for destroying microposts uses Capybara to click the “delete” link and expects the Micropost count to decrease by 1 (Listing 10.45).

	Listing 10.45: Tests for the Microposts controller destroy action.
	spec/requests/micropost_pages_spec.rb
	 require 'spec_helper'

	describe "Micropost pages" do
	  .
	  .
	  .
	  describe "micropost destruction" do
	    before { FactoryGirl.create(:micropost, user: user) }

	    describe "as correct user" do
	      before { visit root_path }

	      it "should delete a micropost" do
	        expect { click_link "delete" }.to change(Micropost, :count).by(-1)
	      end
	    end
	  end
	end

The application code is also analogous to the user case in Listing 9.46; the main difference is that, rather than using an `admin_user` before filter, in the case of microposts we have a **correct_user** before filter to check that the current user actually has a micropost with the given id. The code appears in Listing 10.46, and the result of destroying the second-most-recent post appears in Figure 10.17.

	Listing 10.46: The Microposts controller destroy action.
	app/controllers/microposts_controller.rb
	 class MicropostsController < ApplicationController
	  before_action :signed_in_user, only: [:create, :destroy]
	  before_action :correct_user,   only: :destroy
	  .
	  .
	  .
	  def destroy
	    @micropost.destroy
	    redirect_to root_url
	  end

	  private

	    def micropost_params
	      params.require(:micropost).permit(:content)
	    end

	    def correct_user
	      @micropost = current_user.microposts.find_by(id: params[:id])
	      redirect_to root_url if @micropost.nil?
	    end
	end

In the correct_user before filter, note that we find microposts through the association:

	current_user.microposts.find_by(id: params[:id])

This automatically ensures that we find only microposts belonging to the current user. In this case, we use `find_by` instead of find because the latter raises an exception when the micropost doesn’t exist instead of returning nil. By the way, if you’re comfortable with exceptions in Ruby, you could also write the correct_user filter like this:

	def correct_user
	  @micropost = current_user.microposts.find(params[:id])
	rescue
	  redirect_to root_url
	end

It might occur to you that we could implement the correct_user filter using the Micropost model directly, like this:

	@micropost = Micropost.find_by(id: params[:id])
	redirect_to root_url unless current_user?(@micropost.user)

This would be equivalent to the code in Listing 10.46, but, as explained by [Wolfram Arnold](http://www.rubyfocus.biz/) in the blog post [Access Control 101 in Rails and the Citibank Hack](http://www.rubyfocus.biz/blog/2011/06/15/access_control_101_in_rails_and_the_citibank-hack.html), for security purposes it is a **good practice always to run lookups through the association**.

With the code in this section, our Micropost model and interface are complete, and the test suite should pass:

	$ bundle exec rspec spec/

# 10.4 - Conclusion
With the addition of the Microposts resource, we are nearly finished with our sample application. All that remains is to add a social layer by letting users follow each other. We’ll learn how to model such user relationships, and see the implications for the status feed, in Chapter 11.

Before proceeding, be sure to commit and merge your changes if you’re using Git for version control:

	$ git add .
	$ git commit -m "Add user microposts"
	$ git checkout master
	$ git merge user-microposts
	$ git push

You can also push the app up to Heroku at this point. Because the data model has changed through the addition of the microposts table, you will also need to migrate the production database:

	$ git push heroku
	$ heroku pg:reset DATABASE
	$ heroku run rake db:migrate
	$ heroku run rake db:populate

# 10.5 - Exercises
## Long word
Very long words currently break our layout. Fix this problem using the **wrap** helper defined in Listing 10.47. Note the use of the **raw** method to prevent Rails from escaping the resulting HTML, together with the **sanitize** method needed to prevent **cross-site scripting**. This code also uses the strange-looking but useful **ternary operator** (Box 10.1).

```
There are 10 kinds of people in the world: Those who like the ternary operator, those who don’t, and those who don’t know about it. (If you happen to be in the third category, soon you won’t be any longer.)

When you do a lot of programming, you quickly learn that one of the most common bits of control flow goes something like this:

  if boolean?
    do_one_thing
  else
    do_something_else
  end

Ruby, like many other languages (including C/C++, Perl, PHP, and Java), allows you to replace this with a much more compact expression using the ternary operator (so called because it consists of three parts):

  boolean? ? do_one_thing : do_something_else

You can also use the ternary operator to replace assignment:

  if boolean?
    var = foo
  else
    var = bar
  end

becomes

  var = boolean? ? foo : bar

Another common use is in a function’s return value:

	def foo
	  do_stuff
	  boolean? ? "bar" : "baz"
	end

Since Ruby implicitly returns the value of the last expression in a function, here the foo method returns "bar" or "baz" depending on the value of boolean?. It is this final construction that appears in Listing 10.47.
```

	Listing 10.47: A helper to wrap long words.
	app/helpers/microposts_helper.rb
	 module MicropostsHelper

	  def wrap(content)
	    sanitize(raw(content.split.map{ |s| wrap_long_string(s) }.join(' ')))
	  end

	  private

	    def wrap_long_string(text, max_width = 30)
	      zero_width_space = "&#8203;"
	      regex = /.{1,#{max_width}}/
	      (text.length < max_width) ? text :
	                                  text.scan(regex).join(zero_width_space)
	    end
	end

## Countdown character for microposts
Step 1 : create a **app/javascripts/microposts.js.coffee** file

	updateCountdown = ->
	  remaining = 140 - jQuery("#micropost_content").val().length
	  jQuery(".countdown").text remaining + " characters remaining"

	jQuery ->
	  updateCountdown()
	  $("#micropost_content").change updateCountdown
	  $("#micropost_content").keyup updateCountdown

NB: Being that its placed in the app/javascripts folder, I didn't need to update the application.js file.

Step 2 : update **the _micropost_form.html.erb** partial:

	<%= form_for(@micropost) do |f| %>
	    <%= render 'shared/error_messages', object: f.object %>
	    <div class="field">
	        <%= f.text_area :content, placeholder: "Compose new micropost..." %>
	    </div>
	    <%= f.submit "Post", class: "btn btn-large btn-primary" %>
	    <span class="countdown"></span>
	<% end %>

step 3: implement a bit of css to the **custom_css.css.scss** file

	/* micropost jQuery countdown */

	.countdown {
	  display: inline;
	  padding-left: 10px;
	  color: $grayLight;
	}