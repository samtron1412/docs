[TOC]

In this chapter, we’ll take the first critical step by *creating a data model for users* of our site, together with a way to store that data. In *Chapter 7*, we’ll give users the ability to sign up for our site and create a user profile page. Once users can sign up, we’ll let them sign in and sign out as well (*Chapter 8*), and in *Chapter 9* (Section 9.2.1) we’ll learn how to protect pages from improper access. Taken together, the material in Chapter 6 through Chapter 9 develops a full Rails *login and authentication system*.

Examples of authentication and authorization systems include [Clearance](http://github.com/thoughtbot/clearance), [Authlogic](http://github.com/binarylogic/authlogic), [Devise](http://github.com/plataformatec/devise), and [CanCan](http://railscasts.com/episodes/192-authorization-with-cancan) (as well as non-Rails-specific solutions built on top of [OpenID](http://railscasts.com/episodes/192-authorization-with-cancan) or [OAuth](http://en.wikipedia.org/wiki/Oauth)).

Make a git branch for modeling

	$ git checkout master
	$ git checkout -b modeling-users

# 6.1 - User model
The first step in signing up users is to make a data structure to capture and store their information.

<figure>
  <figcaption style="text-align:center;">Figure 6.1: A mockup of the user signup page.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/signup_mockup_bootstrap.png" alt="signup mockup" title="signup mockup">
</figure>

The default Rails solution to the problem of persistence is to use a database for long-term data storage, and the default library for interacting with the database is called [Active Record](http://en.wikipedia.org/wiki/Active_record_pattern).

Active Record comes with a host of methods for *creating, saving, and finding* data objects, all without having to use the structured query language (SQL) used by relational databases. Moreover, Rails has a feature called **migrations** to allow data definitions to be written in pure Ruby, without having to learn an SQL data definition language (DDL). The effect is that Rails *insulates you almost entirely from the details* of the data store.

## 6.1.1 - Database migrations
	Listing 6.1: Generating a User model.
	$ rails generate model User name:string email:string

(Note that, in contrast to the plural convention for controller names, model names are singular: a *Users* controller, but a *User* model.)

	Listing 6.2: Migration for the User model (to create a users table).
	db/migrate/[timestamp]_create_users.rb
	 class CreateUsers < ActiveRecord::Migration
	  def change
	    create_table :users do |t|
	      t.string :name
	      t.string :email

	      t.timestamps
	    end
	  end
	end

Note that the name of the migration file is prefixed by a **timestamp** based on when the migration was generated. In the early days of migrations, the filenames were prefixed with incrementing integers, which caused conflicts for collaborating teams if multiple programmers had migrations with the same number. Barring the improbable scenario of migrations generated the same second, using timestamps conveniently avoids such collisions.

Here the table name is plural (**users**) even though the model name is singular (*User*), which reflects a linguistic convention followed by Rails: *a model represents a single user*, whereas *a database table consists of many users*. The final line in the block, **t.timestamps**, is a special command that creates two magic columns called `created_at` and `updated_at`, which are timestamps that automatically record when a given user is created and updated.

We can run the migration, known as “*migrating up*”, using the **rake** command as follows:

	$ bundle exec rake db:migrate

Most migrations, including all the ones in the Rails Tutorial, are reversible, which means we can “*migrate down*” and undo them with a single Rake task, called **db:rollback**:

	$ bundle exec rake db:rollback

Under the hood, this command executes the `drop_table` command to remove the users table from the database. The reason this works is that the change method knows that `drop_table` is the inverse of `create_table`, which means that the rollback migration can be easily inferred. In the case of an irreversible migration, such as one to *remove a database column*, it is necessary to define separate **up** and **down** methods in place of the single change method. Read about [migrations in the Rails Guides](http://guides.rubyonrails.org/migrations.html) for more information.

## 6.1.2 - The model file
We begin by looking at the code for the User model, which lives in the file **user.rb** inside the **app/models/ directory**. It is, to put it mildly, very compact (Listing 6.3).

	Listing 6.3: The brand new User model.
	app/models/user.rb
	 class User < ActiveRecord::Base
	end

## 6.1.3 - Creating user objects
 Since we don’t (yet) want to make any changes to our database, we’ll start the console in a sandbox:

	$ rails console --sandbox
	Loading development environment in sandbox
	Any modifications you make will be rolled back on exit
	>>

	>> User.new
	=> #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>

	>> user = User.new(name: "Michael Hartl", email: "mhartl@example.com")
	=> #<User id: nil, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: nil, updated_at: nil>

If you’ve been tailing the development log, you may have noticed that no new lines have shown up yet. This is because calling **User.new** doesn’t touch the database; it simply creates a new Ruby object in memory. To save the user object to the database, we call the **save** method on the user variable:

	>> user.save
	=> true

The save method returns **true** if it succeeds and **false** otherwise. You may have noticed that the new user object had nil values for the **id** and the magic columns `created_at` and `updated_at` attributes. Let’s see if our save changed anything:

	>> user
	=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 00:57:46", updated_at: "2013-03-11 00:57:46">

As we’ll see in Chapter 7, it’s often convenient to make and save a model in two steps as we have above, but Active Record also lets you combine them into one step with **User.create**:

	>> User.create(name: "A Nother", email: "another@example.org")
	#<User id: 2, name: "A Nother", email: "another@example.org", created_at:
	"2013-03-11 01:05:24", updated_at: "2013-03-11 01:05:24">
	>> foo = User.create(name: "Foo", email: "foo@bar.com")
	#<User id: 3, name: "Foo", email: "foo@bar.com", created_at: "2013-03-11
	01:05:42", updated_at: "2013-03-11 01:05:42">

Note that *User.create*, rather than returning true or false, *returns the User object* itself, which we can optionally assign to a variable (such as foo in the second command above).

The inverse of create is destroy:

	>> foo.destroy
	=> #<User id: 3, name: "Foo", email: "foo@bar.com", created_at: "2013-03-11
	01:05:42", updated_at: "2013-03-11 01:05:42">

Oddly, destroy, like create, returns the object in question, though I can’t recall ever having used the return value of destroy. Even odder, perhaps, is that the destroyed object still exists in memory:

	>> foo
	=> #<User id: 3, name: "Foo", email: "foo@bar.com", created_at: "2013-03-11
	01:05:42", updated_at: "2013-03-11 01:05:42">

How do we know if we really destroyed an object? And for saved and non-destroyed objects, how can we retrieve users from the database? It’s time to learn how to use Active Record to find user objects.

## 6.1.4 - Finding user objects
	>> User.find(1)
	=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 00:57:46", updated_at: "2013-03-11 00:57:46">

	>> User.find_by_email("mhartl@example.com")
	=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 00:57:46", updated_at: "2013-03-11 00:57:46">

The **find_by_email** method is automatically created by Active Record based on the email attribute in the users table. (As you might guess, Active Record creates a **find_by_name** method as well.) Starting in Rails 4.0, the preferred method to find by attribute is to use the **find_by** method instead, passing the attribute as a hash:

	>> User.find_by(email: "mhartl@example.com")
	=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 00:57:46", updated_at: "2013-03-11 00:57:46">

If you’re worried that **find_by** will be inefficient if there are a large number of users, you’re ahead of the game; we’ll cover this issue, and its solution via **database indices**, in Section 6.2.5.

	>> User.first
	=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 00:57:46", updated_at: "2013-03-11 00:57:46">

	>> User.all
	=> [#<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 00:57:46", updated_at: "2013-03-11 00:57:46">,
	#<User id: 2, name: "A Nother", email: "another@example.org", created_at:
	"2013-03-11 01:05:24", updated_at: "2013-03-11 01:05:24">]

## 6.1.5 - Updating user objects
First, we can assign attributes individually

	>> user           # Just a reminder about our user's attributes
	=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 00:57:46", updated_at: "2013-03-11 00:57:46">
	>> user.email = "mhartl@example.net"
	=> "mhartl@example.net"
	>> user.save
	=> true

The second main way to update attributes is to use update_attributes:

	>> user.update_attributes(name: "The Dude", email: "dude@abides.org")
	=> true
	>> user.name
	=> "The Dude"
	>> user.email
	=> "dude@abides.org"

# 6.2 - User validations
In this section, we’ll cover several of the most common cases, validating **presence**, **length**, **format** and **uniqueness**. In Section 6.3.4 we’ll add a final common validation, **confirmation**. And we’ll see in Section 7.3 how validations give us convenient error messages when users make submissions that violate them.

## 6.2.1 - Initial user tests
	$ bundle exec rake db:migrate
	$ bundle exec rake test:prepare
	$ bundle exec rspec spec/models/user_spec.rb
	*


	Finished in 0.01999 seconds
	1 example, 0 failures, 1 pending

	Pending:
	  User add some examples to (or delete)
	  /Users/mhartl/rails_projects/sample_app/spec/models/user_spec.rb
	  (Not Yet Implemented)

test file

	Listing 6.5: Testing for the :name and :email attributes.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before { @user = User.new(name: "Example User", email: "user@example.com") }

	  subject { @user }

	  it { should respond_to(:name) }
	  it { should respond_to(:email) }
	end

The `respond_to` methods implicitly use the Ruby method `respond_to?`, which accepts a symbol and returns true if the object responds to the given method or attribute and false otherwise:

	$ rails console --sandbox
	>> user = User.new
	>> user.respond_to?(:name)
	=> true
	>> user.respond_to?(:foobar)
	=> false

## 6.2.2 - Validating presence
Perhaps the most elementary validation is presence, which simply verifies that a given attribute is present. For example, in this section we’ll ensure that both the name and email fields are present before a user gets saved to the database.

	Listing 6.6: Validating the presence of a name attribute.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  validates :name, presence: true
	end

Let try

	$ rails console --sandbox
	>> user = User.new(name: "", email: "mhartl@example.com")
	>> user.save
	=> false
	>> user.valid?
	=> false

error

	>> user.errors.full_messages
	=> ["Name can't be blank"]

## 6.2.3 - Length validation
Test for name length

	Listing 6.11: A test for name length validation.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before do
	    @user = User.new(name: "Example User", email: "user@example.com")
	  end
	  .
	  .
	  .
	  describe "when name is too long" do
	    before { @user.name = "a" * 51 }
	    it { should_not be_valid }
	  end
	end

model file

	Listing 6.12: Adding a length validation for the name attribute.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  validates :name,  presence: true, length: { maximum: 50 }
	  validates :email, presence: true
	end

## 6.2.4 - Format validation
test

	Listing 6.13: Tests for email format validation.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before do
	    @user = User.new(name: "Example User", email: "user@example.com")
	  end
	  .
	  .
	  .
	  describe "when email format is invalid" do
	    it "should be invalid" do
	      addresses = %w[user@foo,com user_at_foo.org example.user@foo.
	                     foo@bar_baz.com foo@bar+baz.com]
	      addresses.each do |invalid_address|
	        @user.email = invalid_address
	        expect(@user).not_to be_valid
	      end
	    end
	  end

	  describe "when email format is valid" do
	    it "should be valid" do
	      addresses = %w[user@foo.COM A_US-ER@f.b.org frst.lst@foo.jp a+b@baz.cn]
	      addresses.each do |valid_address|
	        @user.email = valid_address
	        expect(@user).to be_valid
	      end
	    end
	  end
	end

model file

	Listing 6.14: Validating the email format with a regular expression.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  validates :name,  presence: true, length: { maximum: 50 }
	  VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-]+(\.[a-z]+)+\z/i
	  validates :email, presence: true, format: { with: VALID_EMAIL_REGEX }
	end

meaning of regex

Expression |	Meaning
-|-
/\A[\w+\-.]+@[a-z\d\-]+(\.[a-z]+)+\z/i	| full regex
/	| start of regex
\A	| match start of a string
[\w+\-.]+ |	at least one word character, plus, hyphen, or dot
@	| literal “at sign”
[a-z\d\-]+ |	at least one letter, digit, hyphen
\.	| literal dot
[a-z]+ |	at least one letter
\z	| match end of a string
/	| end of regex
i	| case insensitive

## 6.2.5 - Uniqueness validation
test file

	Listing 6.15: A test for the rejection of duplicate email addresses.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before do
	    @user = User.new(name: "Example User", email: "user@example.com")
	  end

	  subject { @user }
	  .
	  .
	  .
	  describe "when email address is already taken" do
	    before do
	      user_with_same_email = @user.dup
	      user_with_same_email.save
	    end

	    it { should_not be_valid }
	  end
	end

model file

	Listing 6.16: Validating the uniqueness of email addresses.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  .
	  .
	  .
	  validates :email, presence: true, format: { with: VALID_EMAIL_REGEX },
	                    uniqueness: true
	end

We’re not quite done, though. Email addresses are typically processed as if they were case-insensitive—i.e., **foo@bar.com** is treated the same as **FOO@BAR.COM** or **FoO@BAr.coM**—so our validation should incorporate this as well. We test for case-insensitivity with the code in Listing 6.17.

	Listing 6.17: A test for the rejection of duplicate email addresses, insensitive to case.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before do
	    @user = User.new(name: "Example User", email: "user@example.com")
	  end

	  subject { @user }
	  .
	  .
	  .
	  describe "when email address is already taken" do
	    before do
	      user_with_same_email = @user.dup
	      user_with_same_email.email = @user.email.upcase
	      user_with_same_email.save
	    end

	    it { should_not be_valid }
	  end
	end

case-sensitive

	Listing 6.18: Validating the uniqueness of email addresses, ignoring case.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  .
	  .
	  .
	  validates :email, presence: true, format: { with: VALID_EMAIL_REGEX },
	                    uniqueness: { case_sensitive: false }
	end

### The uniqueness caveat
Using **validates :uniqueness** does not guarantee uniqueness.

D’oh! But what can go wrong? Here’s what:

1. Alice signs up for the sample app, with address alice@wonderland.com.
2. Alice accidentally clicks on “Submit” twice, sending two requests in quick succession.
3. The following sequence occurs: request 1 creates a user in memory that passes validation, request 2 does the same, request 1’s user gets saved, request 2’s user gets saved.
4. Result: two user records with the exact same email address, despite the uniqueness validation.

If the above sequence seems implausible, believe me, it isn’t: it can happen on any Rails website with significant traffic. Luckily, the solution is straightforward to implement; we just need to *enforce uniqueness at the database level* as well. Our method is to create a database *index on the email column*, and then require that the index be unique.

we are adding structure to an existing model, so we need to create a migration directly using the **migration** generator:

	$ rails generate migration add_index_to_users_email

	Listing 6.19: The migration for enforcing email uniqueness.
	db/migrate/[timestamp]_add_index_to_users_email.rb
	 class AddIndexToUsersEmail < ActiveRecord::Migration
	  def change
	    add_index :users, :email, unique: true
	  end
	end

migrate darabase

	$ bundle exec rake db:migrate

Unfortunately, there’s one more change we need to make to be assured of email uniqueness, which is to make sure that *the email address is all lower-case before it gets saved to the database*. The reason is that not all database adapters use case-sensitive indices. The way to do this is with a [callback](http://en.wikipedia.org/wiki/Callback_(computer_science)), which is a method that gets invoked at a particular point in the lifetime of an Active Record object (see the [Rails API entry on callbacks](http://api.rubyonrails.org/v4.0.0/classes/ActiveRecord/Callbacks.html)). In the present case, we’ll use a **before_save** callback to force Rails to downcase the email attribute before saving the user to the database, as shown in Listing 6.20.

	Listing 6.20: Ensuring email uniqueness by downcasing the email attribute.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  before_save { self.email = email.downcase }
	  .
	  .
	  .
	end

# 6.3 - Adding a secure password
In this section, we’ll add the last of the basic User attributes: a secure password used to authenticate users of the sample application. The method is to require each user to have a password (with a password confirmation), and then store a *hashed* version of the password in the database.

The method for authenticating users will be to take a submitted password, hash it, and compare the result to the hashed value stored in the database. If the two match, then the submitted password is correct and the user is authenticated. By comparing hashed values instead of raw passwords, we will be able to authenticate users without storing the passwords themselves. This means that, even if our database is compromised, our users’ passwords will still be secure.

Much of the secure password machinery will be implemented using a single Rails method called **has_secure_password** (first introduced in Rails 3.1).

## 6.3.1 - A hashed password
We’ll start with the necessary change to the data model for users, which involves adding a **password_digest** column to the users table.

We’ll use the state-of-the-art hash function called [bcrypt](http://en.wikipedia.org/wiki/Bcrypt) to irreversibly transform the password to make the password hash. To use bcrypt in the sample application, we need to add the **bcrypt-ruby** gem to our **Gemfile** (Listing 6.21).

	Listing 6.21: Adding bcrypt-ruby to the Gemfile.
	source 'https://rubygems.org'
	ruby '2.0.0'
	#ruby-gemset=railstutorial_rails_4_0

	gem 'rails', '4.0.8'
	gem 'bootstrap-sass', '2.3.2.0'
	gem 'sprockets', '2.11.0'
	gem 'bcrypt-ruby', '3.1.2'
	.
	.

run

	$ bundle install

Since we want users to have a password digest column, a user object should respond to **password_digest**

	Listing 6.22: Ensuring that a User object has a password_digest column.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before do
	    @user = User.new(name: "Example User", email: "user@example.com")
	  end

	  subject { @user }

	  it { should respond_to(:name) }
	  it { should respond_to(:email) }
	  it { should respond_to(:password_digest) }
	  .
	  .
	  .
	end

we first generate an appropriate migration for the **password_digest** column:

	$ rails generate migration add_password_digest_to_users password_digest:string

We can choose any migration name we want, but it’s convenient to end the name with `_to_users`, since in this case Rails automatically constructs a migration to add columns to the users table. Moreover, by including the second argument, we’ve given Rails enough information to construct the entire migration for us, as seen in Listing 6.23.

	Listing 6.23: The migration to add a password_digest column to the users table.
	db/migrate/[ts]_add_password_digest_to_users.rb
	 class AddPasswordDigestToUsers < ActiveRecord::Migration
	  def change
	    add_column :users, :password_digest, :string
	  end
	end

	$ bundle exec rake db:migrate
	$ bundle exec rake test:prepare
	$ bundle exec rspec spec/

## 6.3.2 - Password and confirmation
As seen in the mockup in Figure 6.1, we expect to have users confirm their passwords, a common practice on the web meant to minimize typos. We could enforce this at the controller layer, but it’s conventional to put it in the model and use Active Record to enforce the constraint. The method is to add password and password_confirmation attributes to the User model, and then require that the two attributes match before the record is saved to the database. Unlike the other attributes we’ve seen so far, the password attributes will be virtual—they will only exist temporarily in memory, and will not be persisted to the database. As we’ll see in Section 6.3.4, these virtual attributes are implemented automatically by `has_secure_password`.

We’ll start with **respond_to** tests for a password and its confirmation, as seen in Listing 6.24.

	Listing 6.24: Testing for the password and password_confirmation attributes.
	spec/models/user_spec.rb
	 require 'spec_helper'

	describe User do

	  before do
	    @user = User.new(name: "Example User", email: "user@example.com",
	                     password: "foobar", password_confirmation: "foobar")
	  end

	  subject { @user }

	  it { should respond_to(:name) }
	  it { should respond_to(:email) }
	  it { should respond_to(:password_digest) }
	  it { should respond_to(:password) }
	  it { should respond_to(:password_confirmation) }

	  it { should be_valid }
	  .
	  .
	  .
	end

We definitely don’t want users to enter a blank password, so we’ll add another test to validate password presence:

	describe "when password is not present" do
	  before do
	    @user = User.new(name: "Example User", email: "user@example.com",
	                     password: " ", password_confirmation: " ")
	  end
	  it { should_not be_valid }
	end

We also want to ensure that the password and confirmation match.

	describe "when password doesn't match confirmation" do
	  before { @user.password_confirmation = "mismatch" }
	  it { should_not be_valid }
	end

model file

	Listing 6.26: Getting the initial password tests to pass.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  .
	  .
	  .
	  has_secure_password
	end

## 6.3.3 - User authentication
This divides naturally into two parts: first, find a user by email address; second, authenticate the user with a given password.

we can find a user with a given email address using the **find_by** method:

	user = User.find_by(email: email)

The second step is then to use an **authenticate** method to verify that the user has the given password. In Chapter 8, we’ll retrieve the current (signed-in) user using code something like this:

	current_user = user.authenticate(password)

If the given password matches the user’s password, it should return the user; otherwise, it should return **false**.

test file

	.
	it { should respond_to(:authenticate) }
	.
	.
	describe "return value of authenticate method" do
	  before { @user.save }
	  let(:found_user) { User.find_by(email: @user.email) }

	  describe "with valid password" do
	    it { should eq found_user.authenticate(@user.password) }
	  end

	  describe "with invalid password" do
	    let(:user_for_invalid_password) { found_user.authenticate("invalid") }

	    it { should_not eq user_for_invalid_password }
	    specify { expect(user_for_invalid_password).to be_false }
	  end
	end

the **specify** method. This is just a synonym for it, and can be used when writing it would sound unnatural. In this case, it sounds OK to say “it [i.e., the user] should not equal user for invalid password”, but it sounds strange to say “it user for invalid password should be false”; saying “**specify**: expect user for invalid password to be false” sounds better.

Finally, as a security precaution, we’ll test for a length validation on passwords, requiring that they be at least six characters long:

	describe "with a password that's too short" do
	  before { @user.password = @user.password_confirmation = "a" * 5 }
	  it { should be_invalid }
	end

## 6.3.4 - User has secure password
I suggest taking a look at the [source code for secure_password.rb](https://github.com/rails/rails/blob/master/activemodel/lib/active_model/secure_password.rb), which is well-documented and quite readable. That code includes the lines

	validates_confirmation_of :password,
                          if: lambda { |m| m.password.present? }

which (as described in the [Rails API](http://api.rubyonrails.org/v4.0.0/classes/ActiveModel/Validations/HelperMethods.html#method-i-validates_confirmation_of)) automagically creates an attribute called `password_confirmation`. It also includes a validation for the **password_digest** attribute.)

User model

	Listing 6.29: The complete implementation for secure passwords.
	app/models/user.rb
	 class User < ActiveRecord::Base
	  before_save { self.email = email.downcase }
	  validates :name, presence: true, length: { maximum: 50 }
	  VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
	  validates :email, presence:   true,
	                    format:     { with: VALID_EMAIL_REGEX },
	                    uniqueness: { case_sensitive: false }
	  has_secure_password
	  validates :password, length: { minimum: 6 }
	end

## 6.3.5 - Creating a user
	$ rails console
	>> User.create(name: "Michael Hartl", email: "mhartl@example.com",
	?>             password: "foobar", password_confirmation: "foobar")

Use **pgAdmin3** to view PostgreSQL databases or use **psql**

	>> user = User.find_by(email: "mhartl@example.com")
	>> user.password_digest
	=> "$2a$10$kn4cQDJTzV76ZgDxOWk6Je9A0Ttn5sKNaGTEmT0jU7.ncBJ/60gHq"

	>> user.authenticate("invalid")
	=> false
	>> user.authenticate("foobar")
	=> #<User id: 1, name: "Michael Hartl", email: "mhartl@example.com",
	created_at: "2013-03-11 20:45:19", updated_at: "2013-03-11 20:45:19",
	password_digest: "$2a$10$kn4cQDJTzV76ZgDxOWk6Je9A0Ttn5sKNaGTEmT0jU7.n...">

# 6.4 - Conclusion
Starting from scratch, in this chapter we created a working User model with **name**, **email**, and various password attributes, together with validations enforcing several important constraints on their values. In addition, we can securely authenticate users using a given password. In previous versions of Rails, such a feat would have taken more than twice as much code, but because of the compact **validates** method and **has_secure_password**, we were able to build a complete User model using less than a dozen lines of code.

In the next chapter, Chapter 7, we’ll make a working signup form to create new users, together with a page to display each user’s information. In Chapter 8, we’ll use the authentication machinery from Section 6.3 to let users sign into the site.

If you’re using Git, now would be a good time to commit if you haven’t done so in a while:

	$ git add .
	$ git commit -m "Make a basic User model (including secure passwords)"

Then merge back into the master branch:

	$ git checkout master
	$ git merge modeling-users

# 6.5 - Exercises