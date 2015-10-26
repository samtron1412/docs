[TOC]

This chapter explores some elements of Ruby important for Rails. Ruby is a big language, but fortunately the subset needed to be productive as a Rails developer is relatively small. Moreover, this subset is different from the usual approaches to learning Ruby, which is why, if your goal is *making dynamic web applications*, I recommend learning Rails first, picking up bits of Ruby along the way. To become a Rails expert, you need to understand Ruby more deeply, and this book gives you a good foundation for developing that expertise.

# 4.1 - Motivation
When we last saw our new application:

	Listing 4.1:
	<!DOCTYPE html>
	<html>
	  <head>
	    <title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>
	    <%= stylesheet_link_tag "application", media: "all",
	                                           "data-turbolinks-track" => true %>
	    <%= javascript_include_tag "application", "data-turbolinks-track" => true %>
	    <%= csrf_meta_tags %>
	  </head>
	  <body>
	    <%= yield %>
	  </body>
	</html>

Let's focus on one particular line:

	<%= stylesheet_link_tag "application", media: "all", "data-turbolinks-track" => true %>

This uses the built-in Rails function **stylesheet_link_tag** (which you can read more about at the [Rails API](http://api.rubyonrails.org/classes/ActionView/Helpers/AssetTagHelper.html#method-i-stylesheet_link_tag)) to include **application.css** for all media types (including computer screens and printers).

There are at least four potentially confusing Ruby ideas: **built-in Rails methods**, **method invocation with missing parentheses**, **symbols**, and **hashes**. We’ll cover all of these ideas in this chapter.

In addition to coming equipped with a large number of built-in functions for use in the views, Rails also allows the creation of new ones. Such functions are called **helpers**; to see how to make a custom helper, let’s start by examining the title line:

	Ruby on Rails Tutorial Sample App | <%= yield(:title) %>

This relies on the definition of a page title (using **provide**) in each view, as in:

	<% provide(:title, 'Home') %>

But what if we don’t provide a title? It’s a good convention to have a *base title* we use on every page, with an optional page title if we want to be more specific. We’ve almost achieved that with our current layout, with one *wrinkle*: as you can see if you delete the provide call in one of the views, *in the absence of a page-specific title* the full title appears as follows:

	Ruby on Rails Tutorial Sample App |

In other words, there’s a suitable base title, but there’s also a trailing vertical bar character `|` at the end. To solve the problem of a missing page title, we’ll define a custom helper called `full_title`. The *full_title helper* returns a base title, “Ruby on Rails Tutorial Sample App”, if no page title is defined, and adds a vertical bar followed by the page title if one is defined:

	Listing 4.2: Defining a full_title helper.
	app/helpers/application_helper.rb

	module ApplicationHelper
	  # Returns the full title on a per-page basis.
	  def full_title(page_title)
	    base_title = "Ruby on Rails Tutorial Sample App"
	    if page_title.empty?
	      base_title
	    else
	      "#{base_title} | #{page_title}"
	    end
	  end
	end

Now that we have a helper, we can use it to simplify our layout by replacing

	<title>Ruby on Rails Tutorial Sample App | <%= yield(:title) %></title>

with

	<title><%= full_title(yield(:title)) %></title>

as seen in Listing 4.3.

	Listing 4.3: The sample application site layout.
	app/views/layouts/application.html.erb

	<!DOCTYPE html>
	<html>
	  <head>
	    <title><%= full_title(yield(:title)) %></title>
	    <%= stylesheet_link_tag "application", media: "all",
	                                           "data-turbolinks-track" => true %>
	    <%= javascript_include_tag "application", "data-turbolinks-track" => true %>
	    <%= csrf_meta_tags %>
	  </head>
	  <body>
	    <%= yield %>
	  </body>
	</html>

Updating our test code:

	Listing 4.4: Updated tests for the Home page’s title.
	spec/requests/static_pages_spec.rb

	describe "Home page" do
	  it "should have the content 'Sample App'" do
	    visit '/static_pages/home'
	    expect(page).to have_content('Sample App')
	  end
	  it "should have the base title" do
	    visit '/static_pages/home'
	    expect(page).to have_title("#{base_title}")
	  end
	  it "should not have a custom page title" do
	    visit '/static_pages/home'
	    expect(page).not_to have_title('| Home')
	  end
	end

Let’s run the test suite to verify that one test fails:

	click mouse to describe block and hit "Ctrl-Shift-R"

To get the test suite to pass, we’ll remove the **provide** line from the Home page’s view, as seen in Listing 4.5.

	Listing 4.5: The Home page with no custom page title.
	app/views/static_pages/home.html.erb

	<h1>Sample App</h1>
	<p>
	  This is the home page for the
	  <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	  sample application.
	</p>

At this point the tests should pass.

	click mouse to describe block and hit "Ctrl-Shift-E"

As with the line to include the application stylesheet, the code in Listing 4.2 may look simple to the eyes of an experienced Rails developer, but it’s full of potentially confusing Ruby ideas: **modules**, **comments**, **local variable assignment**, **booleans**, **control flow**, **string interpolation**, and **return values**. This chapter will cover all of these ideas as well.

# 4.2 - Strings and methods
Our principal tool for learning Ruby will be the *Rails console*, a command-line tool for interacting with Rails applications first seen in Section 2.3.3. The console itself is built on top of interactive Ruby (**irb**), and thus has access to the full power of the Ruby language. (As we’ll see in Section 4.4.4, the console also has access to the Rails environment.) Start the console at the command line as follows:

	$ rails console
	Loading development environment
	>>

By default, the console starts in a **development** environment, which is one of three separate environments defined by Rails (the others are test and production). This distinction won’t be important in this chapter, but we’ll learn more about environments in Section 7.1.1.

When using the console, type **Ctrl-C** if you get stuck, or **Ctrl-D** to exit the console altogether. Throughout the rest of this chapter, you might find it helpful to consult the [Ruby API](http://ruby-doc.org/core-2.0.0/). It’s packed (perhaps even too packed) with information; for example, to learn more about Ruby strings you can look at the Ruby API entry for the **String** class.

## 4.2.1 - Comments
Ruby comments start with the **pound sign #** (also called the “*hash mark*” or, more poetically, the *“octothorpe”*) and extend to the end of the line.

## 4.2.2 - Strings
Strings are probably the most important data structure for web applications, since web pages ultimately consist of strings of characters sent from the server to the browser.

We can also concatenate strings with the + operator:

	>> "foo" + "bar"    # String concatenation
	=> "foobar"

Another way to build up strings is via interpolation using the special syntax **#{}**:

	>> first_name = "Michael"    # Variable assignment
	=> "Michael"
	>> "#{first_name} Hartl"     # String interpolation
	=> "Michael Hartl"

### Printing
	>> print "foo"    # print string (same as puts, but without the newline)
	foo=> nil
	>> print "foo\n"  # Same as puts "foo"
	foo
	=> nil

### Single-quoted strings
	>> '#{foo} bar'     # Single-quoted strings don't allow interpolation
	=> "\#{foo} bar"

	>> '\n'       # A literal 'backslash n' combination
	=> "\\n"

	>> 'Newlines (\n) and tabs (\t) both use the backslash character \.'
	=> "Newlines (\\n) and tabs (\\t) both use the backslash character \\."

## 4.2.3 - Objects and message passing

## 4.2.4 - Method definitions

# 4.3 - Other data structures
## 4.3.1 - Arrays and ranges
strings to array

	>>  "foo bar     baz".split     # Split a string into a three-element array.
	=> ["foo", "bar", "baz"]

	>> "fooxbarxbazx".split('x')
	=> ["foo", "bar", "baz"]

array to strings

	>> a
	=> [42, 8, 17, 7, "foo", "bar"]
	>> a.join                       # Join on nothing.
	=> "428177foobar"
	>> a.join(', ')                 # Join on comma-space.
	=> "42, 8, 17, 7, foo, bar"

other

	>> a = [42, 8, 17]
	=> [42, 8, 17]
	>> a[0]               # Ruby uses square brackets for array access.
	=> 42
	>> a[1]
	=> 8
	>> a[2]
	=> 17
	>> a[-1]              # Indices can even be negative!
	=> 17

use some extension of Rails added to ruby

	>> a                  # Just a reminder of what 'a' is
	=> [42, 8, 17]
	>> a.first
	=> 42
	>> a.second
	=> 8
	>> a.last
	=> 17
	>> a.last == a[-1]    # Comparison using ==
	=> true

	>> x = a.length       # Like strings, arrays respond to the 'length' method.
	=> 3
	>> x == 3
	=> true
	>> x == 1
	=> false
	>> x != 1
	=> true
	>> x >= 1
	=> true
	>> x < 1
	=> false

	>> a
	=> [42, 8, 17]
	>> a.sort
	=> [8, 17, 42]
	>> a.reverse
	=> [17, 8, 42]
	>> a.shuffle
	=> [17, 42, 8]
	>> a
	=> [42, 8, 17]

Note that none of the methods above changes a itself. To **mutate** the array, use the corresponding *“bang”* methods (so-called because the exclamation point is usually pronounced “bang” in this context):

	>> a
	=> [42, 8, 17]
	>> a.sort!
	=> [8, 17, 42]
	>> a
	=> [8, 17, 42]


	>> a.push(6)                  # Pushing 6 onto an array
	=> [42, 8, 17, 6]
	>> a << 7                     # Pushing 7 onto an array
	=> [42, 8, 17, 6, 7]
	>> a << "foo" << "bar"        # Chaining array pushes
	=> [42, 8, 17, 6, 7, "foo", "bar"]

Closely related to arrays are **ranges**, which can probably most easily be understood by converting them to arrays using the **to_a** method:

	>> 0..9
	=> 0..9
	>> 0..9.to_a              # Oops, call to_a on 9.
	NoMethodError: undefined method `to_a' for 9:Fixnum
	>> (0..9).to_a            # Use parentheses to call to_a on the range.
	=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

	>> a = %w[foo bar baz quux]         # Use %w to make a string array.
	=> ["foo", "bar", "baz", "quux"]
	>> a[0..2]
	=> ["foo", "bar", "baz"]

	>> a = (0..9).to_a
	=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
	>> a[2..(a.length-1)]               # Explicitly use the array's length.
	=> [2, 3, 4, 5, 6, 7, 8, 9]
	>> a[2..-1]                         # Use the index -1 trick.
	=> [2, 3, 4, 5, 6, 7, 8, 9]

	>> ('a'..'e').to_a
	=> ["a", "b", "c", "d", "e"]

## 4.3.2 - Blocks
Both arrays and ranges respond to a host of methods that accept blocks, which are simultaneously one of Ruby’s most powerful and most confusing features:

	>> (1..5).each { |i| puts 2 * i }
	2
	4
	6
	8
	10
	=> 1..5

This code calls the **each** method on the **range** `(1..5)` and passes it the **block** `{ |i| puts 2 * i }`. The vertical bars around the variable name in **|i|** are Ruby syntax for a **block variable**, and it’s up to the method to know what to do with the block. In this case, the range’s each method can handle a block with a single local variable, which we’ve called i, and it just executes the block for each value in the range.

second way to indicate a block:

	>> (1..5).each do |i|
	?>   puts 2 * i
	>> end
	2
	4
	6
	8
	10
	=> 1..5

Blocks can be more than one line, and often are. In the Rails Tutorial we’ll follow the common convention of using curly braces only for short one-line blocks and the do..end syntax for longer one-liners and for multi-line blocks.

	>> 3.times { puts "Betelgeuse!" }   # 3.times takes a block with no variables.
	"Betelgeuse!"
	"Betelgeuse!"
	"Betelgeuse!"
	=> 3
	>> (1..5).map { |i| i**2 }          # The ** notation is for 'power'.
	=> [1, 4, 9, 16, 25]
	>> %w[a b c]                        # Recall that %w makes string arrays.
	=> ["a", "b", "c"]
	>> %w[a b c].map { |char| char.upcase }
	=> ["A", "B", "C"]
	>> %w[A B C].map { |char| char.downcase }
	=> ["a", "b", "c"]

As you can see, the map method returns the result of applying the given block to each element in the array or range.

## 4.3.3 - Hashes and symbols
**Hashes** are essentially *arrays that aren’t limited to integer indices*. (In fact, some languages, especially Perl, sometimes call hashes *associative arrays* for this reason.) Instead, *hash indices, or keys, can be almost any object*. For example, we can use strings as keys:

	>> user = {}                          # {} is an empty hash.
	=> {}
	>> user["first_name"] = "Michael"     # Key "first_name", value "Michael"
	=> "Michael"
	>> user["last_name"] = "Hartl"        # Key "last_name", value "Hartl"
	=> "Hartl"
	>> user["first_name"]                 # Element access is like arrays.
	=> "Michael"
	>> user                               # A literal representation of the hash
	=> {"last_name"=>"Hartl", "first_name"=>"Michael"}

Since it’s so common for hashes to use symbols as keys, Ruby 1.9 supports a new syntax just for this special case:

	>> h1 = { :name => "Michael Hartl", :email => "michael@example.com" }
	=> {:name=>"Michael Hartl", :email=>"michael@example.com"}
	>> h2 = { name: "Michael Hartl", email: "michael@example.com" }
	=> {:name=>"Michael Hartl", :email=>"michael@example.com"}
	>> h1 == h2
	=> true

Unfortunately, this can be confusing, especially since :name is valid on its own (as a standalone symbol) but name: has no meaning by itself. The bottom line is that :name => and name: are effectively the same only inside literal hashes, so that

	{ :name => "Michael Hartl" }

and

	{ name: "Michael Hartl" }

are equivalent, but otherwise you need to use :name (with the colon coming first) to denote a symbol.

Hash values can be virtually anything, even other hashes:

	>> params = {}        # Define a hash called 'params' (short for 'parameters').
	=> {}
	>> params[:user] = { name: "Michael Hartl", email: "mhartl@example.com" }
	=> {:name=>"Michael Hartl", :email=>"mhartl@example.com"}
	>> params
	=> {:user=>{:name=>"Michael Hartl", :email=>"mhartl@example.com"}}
	>>  params[:user][:email]
	=> "mhartl@example.com"

These sorts of hashes-of-hashes, or nested hashes, are heavily used by Rails, as we’ll see starting in Section 7.3.

As with arrays and ranges, hashes respond to the **each** method. For example, consider a hash named **flash** with keys for two conditions, **:success** and **:error**:

	>> flash = { success: "It worked!", error: "It failed." }
	=> {:success=>"It worked!", :error=>"It failed."}
	>> flash.each do |key, value|
	?>   puts "Key #{key.inspect} has value #{value.inspect}"
	>> end
	Key :success has value "It worked!"
	Key :error has value "It failed."

Note that, while the **each** method for arrays takes a block with *only one variable,* each for *hashes takes two, a key and a value*. Thus, the each method for a hash iterates through the hash one key-value pair at a time.

The last example uses the useful **inspect** method, which returns a string with a literal representation of the object it’s called on:

	>> puts (1..5).to_a            # Put an array as a string.
	1
	2
	3
	4
	5
	>> puts (1..5).to_a.inspect    # Put a literal array.
	[1, 2, 3, 4, 5]
	>> puts :name, :name.inspect
	name
	:name
	>> puts "It worked!", "It worked!".inspect
	It worked!
	"It worked!"

By the way, using **inspect** to print an object is common enough that there’s a shortcut for it, the **p** function:

	>> p :name             # Same as 'puts :name.inspect'
	:name

## 4.3.4 - CSS revisited
It’s time now to revisit the line from Listing 4.1 used in the layout to include the **cascading style sheets**:

	<%= stylesheet_link_tag "application", media: "all", "data-turbolinks-track" => true %>

Rails defines a special function to include stylesheets, and

	stylesheet_link_tag "application", media: "all", "data-turbolinks-track" => true

is a call to this function. But there are several mysteries. First, where are the parentheses? In Ruby, they are optional; these two are equivalent:

    # Parentheses on function calls are optional.
	stylesheet_link_tag("application", media: "all",
	                                   "data-turbolinks-track" => true)
	stylesheet_link_tag "application", media: "all",
	                                   "data-turbolinks-track" => true

Second, the **media** argument sure looks like a hash, but where are the curly braces? When hashes are the last argument in a function call, the curly braces are optional; these two are equivalent:

    # Curly braces on final hash arguments are optional.
	stylesheet_link_tag "application", { media: "all",
	                                     "data-turbolinks-track" => true }
	stylesheet_link_tag "application", media: "all",
	                                   "data-turbolinks-track" => true

Next, why does the data-turbolinks-track key/value pair use the old-style hashrocket syntax? This is because using the newer syntax to write:

	data-turbolinks-track: true

is invalid because of the hyphens. This forces us to use the older syntax, yielding

	"data-turbolinks-track" => true

Finally, why does Ruby correctly interpret the lines

	stylesheet_link_tag "application", media: "all",
	                                   "data-turbolinks-track" => true

even with a line break between the final elements? The answer is that Ruby doesn’t distinguish between newlines and other whitespace in this context.

So, we see now that the line

	stylesheet_link_tag "application", media: "all",
	                                   "data-turbolinks-track" => true

calls the **stylesheet_link_tag** function with two arguments: a string, indicating the path to the stylesheet, and a hash with two elements, indicating the media type and telling Rails to use the [turbolinks](https://github.com/rails/turbolinks) feature (new in Rails 4). (Turbolinks will be described in more detail in a future draft of this book.) Because of the **<%= %>** brackets, the results are inserted into the template by ERb, and if you view the source of the page in your browser you should see the HTML needed to include a stylesheet (Listing 4.7). (You may see some extra things, like **?body=1**, after the CSS filenames. These are inserted by Rails to ensure that browsers reload the CSS when it changes on the server.)

	Listing 4.7: The HTML source produced by the CSS includes.

	<link data-turbolinks-track="true" href="/assets/application.css" media="all"
	rel="stylesheet" />

# 4.4 - Ruby classes
Ruby, like many object-oriented languages, uses classes to organize methods; these classes are then instantiated to create objects.

## 4.4.1 - Constructors
we instantiated a string using the double quote characters, which is a literal constructor for strings:

	>> s = "foobar"       # A literal constructor for strings using double quotes
	=> "foobar"
	>> s.class
	=> String

Instead of using a **literal constructor**, we can use the equivalent **named constructor**, which involves calling the **new** method on the class name:

	>> s = String.new("foobar")   # A named constructor for a string
	=> "foobar"
	>> s.class
	=> String
	>> s == "foobar"
	=> true

Arrays work the same way as strings:

	>> a = Array.new([1, 3, 2])
	=> [1, 3, 2]

Hashes, in contrast, are different. While the array constructor **Array.new** takes an initial value for the array, **Hash.new** takes a default value for the hash, which is the value of the hash for a nonexistent key:

	>> h = Hash.new
	=> {}
	>> h[:foo]            # Try to access the value for the nonexistent key :foo.
	=> nil
	>> h = Hash.new(0)    # Arrange for nonexistent keys to return 0 instead of nil.
	=> {}
	>> h[:foo]
	=> 0
	>> h[:bar]
	=> 0
	>> h = Hash.new(1)    # Arrange for nonexistent keys to return 1 instead of nil.
	=> {}
	>> h[:foo]
	=> 1
	>> h[:bar]
	=> 1

When a method gets called on the class itself, as in the case of **new**, it’s called a **class method**. The result of calling new on a class is an object of that class, also called an *instance* of the class. A method called on an instance, such as **length**, is called an **instance method**.

## 4.4.2 - Class inheritance
When learning about classes, it’s useful to find out the **class hierarchy** using the **superclass** method:

	>> s = String.new("foobar")
	=> "foobar"
	>> s.class                        # Find the class of s.
	=> String
	>> s.class.superclass             # Find the superclass of String.
	=> Object
	>> s.class.superclass.superclass  # Ruby 1.9 uses a new BasicObject base class
	=> BasicObject
	>> s.class.superclass.superclass.superclass
	=> nil

To understand classes a little more deeply, there’s no substitute for making one of our own. Let’s make a **Word** class with a **palindrome?** method that returns true if the word is the same spelled forward and backward:

	>> class Word
	>>   def palindrome?(string)
	>>     string == string.reverse
	>>   end
	>> end
	=> nil

We can use it as follows:

	>> w = Word.new              # Make a new Word object.
	=> #<Word:0x22d0b20>
	>> w.palindrome?("foobar")
	=> false
	>> w.palindrome?("level")
	=> true

Since a word is a string, it’s more natural to have our **Word** class inherit from **String**, as seen in Listing 4.8. (You should exit the console and re-enter it to clear out the old definition of Word.)

	Listing 4.8: Defining a Word class in the console.
	>> class Word < String             # Word inherits from String.
	>>   # Returns true if the string is its own reverse.
	>>   def palindrome?
	>>     self == self.reverse        # self is the string itself.
	>>   end
	>> end
	=> nil

	>> s = Word.new("level")    # Make a new Word, initialized with "level".
	=> "level"
	>> s.palindrome?            # Words have the palindrome? method.
	=> true
	>> s.length                 # Words also inherit all the normal string methods.
	=> 5

**self** is the object itself.

## 4.4.3 - Modifying built-in classes
While inheritance is a powerful idea, in the case of palindromes it might be even more natural to add the **palindrome?** method to the **String** class itself, so that (among other things) we can call **palindrome?** on a string literal, which we currently can’t do:

	>> "level".palindrome?
	NoMethodError: undefined method `palindrome?' for "level":String

Amazingly, Ruby lets you do just this; Ruby classes can be *opened* and *modified*, allowing ordinary mortals such as ourselves to add methods to them:

	>> class String
	>>   # Returns true if the string is its own reverse.
	>>   def palindrome?
	>>     self == self.reverse
	>>   end
	>> end
	=> nil
	>> "deified".palindrome?
	=> true

Modifying built-in classes is a powerful technique, but with *great power comes great responsibility*, and it’s considered bad form to add methods to built-in classes without having a really *good reason* for doing so. Rails does have some good reasons; for example, in web applications we often want to prevent variables from being blank—e.g., a user’s name should be something other than spaces and other whitespace—so Rails adds a **blank?** method to Ruby. Since the Rails console automatically includes the Rails extensions, we can see an example here (this won’t work in plain **irb**):

	>> "".blank?
	=> true
	>> "      ".empty?
	=> false
	>> "      ".blank?
	=> true
	>> nil.blank?
	=> true

We see that a string of spaces is not *empty*, but it is *blank*. Note also that **nil** is blank; since **nil** isn’t a string, this is a hint that Rails actually adds **blank?** to **String**’s base class, which (as we saw at the beginning of this section) is **Object** itself. We’ll see some other examples of Rails additions to Ruby classes in Section 8.2.1.

## 4.4.4 - A controller class
Since *each Rails console session loads the local Rails environment*, we can even create a controller explicitly and examine its class hierarchy:

	>> controller = StaticPagesController.new
	=> #<StaticPagesController:0x22855d0>
	>> controller.class
	=> StaticPagesController
	>> controller.class.superclass
	=> ApplicationController
	>> controller.class.superclass.superclass
	=> ActionController::Base
	>> controller.class.superclass.superclass.superclass
	=> ActionController::Metal
	>> controller.class.superclass.superclass.superclass.superclass
	=> AbstractController::Base
	>> controller.class.superclass.superclass.superclass.superclass.superclass
	=> Object
	>> controller.class.superclass.superclass.superclass.superclass.superclass.superclass
	=> BasicObject

We can even call the controller *actions* inside the console, which are just methods:

	>> controller.home
	=> nil

Here the return value is **nil** because the home action is blank.

But wait—actions don’t have return values, at least not ones that matter. The point of the home action, as we saw in Chapter 3, is to render a web page, not to return a value. And I sure don’t remember ever calling **StaticPagesController.new** anywhere. What’s going on?

What’s going on is that Rails is written in Ruby, but Rails isn’t Ruby. Some Rails classes are used like ordinary Ruby objects, but some are just *grist* for Rails’ magic mill. Rails is [sui generis](http://en.wikipedia.org/wiki/Sui_generis)(dac trung rieng biet), and should be studied and understood separately from Ruby.

## 4.4.5 - A user class
We end our tour of Ruby with a complete class of our own, a **User** class that anticipates the User model coming up in Chapter 6.

So far we’ve entered class definitions at the console, but this quickly becomes tiresome; instead, create the file **example_user.rb** in your application root directory and fill it with the contents of Listing 4.9.

	Listing 4.9: Code for an example user.
	example_user.rb
	 class User
	  attr_accessor :name, :email

	  def initialize(attributes = {})
	    @name  = attributes[:name]
	    @email = attributes[:email]
	  end

	  def formatted_email
	    "#{@name} <#{@email}>"
	  end
	end

There’s quite a bit going on here, so let’s take it step by step. The first line,

	attr_accessor :name, :email

creates attribute [accessors](http://en.wikipedia.org/wiki/Accessor) corresponding to a user’s name and email address. This creates *“getter”* and *“setter”* methods that allow us to retrieve (get) and assign (set) **@name** and **@email** instance variables. In Rails, the principal importance of instance variables is that they are automatically available in the views, but in general they are used for variables that *need to be available throughout a Ruby class*. Instance variables always begin with an **@** sign, and are **nil** when undefined.

The first method, **initialize**, is special in Ruby: it’s the method called when we execute **User.new**. This particular **initialize** takes one argument, **attributes**:

	def initialize(attributes = {})
	    @name  = attributes[:name]
	    @email = attributes[:email]
	  end

Here the **attributes** variable has a *default value* equal to the empty hash, so that we can define a user with no name or email address (recall from Section 4.3.3 that hashes return **nil** for nonexistent keys, so **attributes[:name]** will be **nil** if there is no **:name** key, and similarly for **attributes[:email]**).

Finally, our class defines a method called **formatted_email** that uses the values of the assigned **@name** and **@email** variables to build up a nicely formatted version of the user’s email address using *string interpolation*

	def formatted_email
	    "#{@name} <#{@email}>"
	  end

Let’s fire up the console, **require** the example user code, and take our User class out for a spin:

	>> require './example_user'     # This is how you load the example_user code.
	=> ["User"]
	>> example = User.new
	=> #<User:0x224ceec @email=nil, @name=nil>
	>> example.name                 # nil since attributes[:name] is nil
	=> nil
	>> example.name = "Example User"           # Assign a non-nil name
	=> "Example User"
	>> example.email = "user@example.com"      # and a non-nil email address
	=> "user@example.com"
	>> example.formatted_email
	=> "Example User <user@example.com>"

Recalling from Section 4.3.4 we can omit the curly braces for final hash arguments, we can create another user by passing a hash to the **initialize** method to create a user with pre-defined attributes:

	>> user = User.new(name: "Michael Hartl", email: "mhartl@example.com")
	=> #<User:0x225167c @email="mhartl@example.com", @name="Michael Hartl">
	>> user.formatted_email
	=> "Michael Hartl <mhartl@example.com>"

We will see starting in Chapter 7 that initializing objects using a hash argument, a technique known as *mass assignment*, is common in Rails applications.

# 4.5 - Conclusion
We won’t be using the **example_user.rb** file from Section 4.4.5, so I suggest removing it:

	$ rm example_user.rb

Then commit the other changes to the main source code repository:

	$ git add .
	$ git commit -m "Add a full_title helper"

# 4.6 - Exercises
