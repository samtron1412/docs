[TOC]

In the process of taking a brief tour of Ruby in Chapter 4, we learned about including the application *stylesheet* into the sample application—but, as noted in Section 4.3.4, this stylesheet is currently empty. In this chapter, we’ll change this by *incorporating the Bootstrap framework* into our application, and then we’ll *add some custom styles* of our own. We’ll also start filling in the layout with links to the pages (such as Home and About) that we’ve created so far (Section 5.1). Along the way, we’ll learn about *partials*, *Rails routes*, and the *asset pipeline*, including an introduction to *Sass* (Section 5.2). We’ll also refactor the tests from Chapter 3 using the *latest RSpec techniques*. We’ll end by *taking a first important step toward letting users sign up* to our site.

# 5.1 - Adding some structure
In addition to using some custom CSS rules, we’ll make use of [Bootstrap](http://getbootstrap.com/), an open-source web design framework from Twitter. We’ll also give our code some styling, so to speak, using *partials* to tidy up the layout once *it gets a little cluttered*.

When building web applications, it is often useful to *get a high-level overview of the user interface as early as possible*. Throughout the rest of this book, I will thus often include [mockups](http://en.wikipedia.org/wiki/Mockup) (in a web context often called *wireframes*), which are *rough sketches* of what the eventual application will look like. The mockups in the *Ruby on Rails Tutorial* are made with an excellent online mockup application called [Mockingbird](https://gomockingbird.com/).

In this chapter, we will principally be developing the static pages introduced in Section 3.1, including a *site logo*, a *navigation header*, and a *site footer*. A mockup for the most important of these pages, the Home page, appears in Figure 5.1. You can see the final result in Figure 5.7. You’ll note that it differs in some details—for example, we’ll end up adding a Rails logo on the page—but that’s fine, since a mockup need not be exact.

<figure>
  <figcaption style="text-align:center;">A mockup of the sample application’s Home page.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/home_page_mockup_bootstrap.png" alt="mockup" title="mockup">
</figure>

As usual, if you’re using Git for version control, now would be a good time to make a new branch:

	$ git checkout -b filling-in-layout

## 5.1.1 - Site navigation
As a first step toward adding links and styles to the sample application, we’ll update the site layout file **application.html.erb** (last seen in Listing 4.3) with additional HTML structure. This includes some additional *divisions*, *some CSS classes*, and the start of our site navigation. The full file is in Listing 5.1; explanations for the various pieces follow immediately thereafter.

	Listing 5.1: The site layout with added structure.
	app/views/layouts/application.html.erb
	 <!DOCTYPE html>
	<html>
	  <head>
	    <title><%= full_title(yield(:title)) %></title>
	    <%= stylesheet_link_tag "application", media: "all",
	                                           "data-turbolinks-track" => true %>
	    <%= javascript_include_tag "application", "data-turbolinks-track" => true %>
	    <%= csrf_meta_tags %>
	    <!--[if lt IE 9]>
	    <script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
	    <![endif]-->
	  </head>
	  <body>
	    <header class="navbar navbar-fixed-top navbar-inverse">
	      <div class="navbar-inner">
	        <div class="container">
	          <%= link_to "sample app", '#', id: "logo" %>
	          <nav>
	            <ul class="nav pull-right">
	              <li><%= link_to "Home",    '#' %></li>
	              <li><%= link_to "Help",    '#' %></li>
	              <li><%= link_to "Sign in", '#' %></li>
	            </ul>
	          </nav>
	        </div>
	      </div>
	    </header>
	    <div class="container">
	      <%= yield %>
	    </div>
	  </body>
	</html>

Let’s look at the new elements in Listing 5.1 from top to bottom. As *alluded* to briefly in Section 3.3.2, *Rails 4 uses HTML5 by default* (as indicated by the doctype **<!DOCTYPE html>**); since the HTML5 standard is relatively new, some browsers (especially older versions Internet Explorer) don’t fully support it, so we include some JavaScript code (known as an “[HTML5 shim](http://code.google.com/p/html5shim/)”) to work around the issue:

	<!--[if lt IE 9]>
	<script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
	<![endif]-->

The somewhat odd syntax

	<!--[if lt IE 9]>

The weird **[if lt IE 9]** syntax is not part of Rails; it’s actually a [conditional comment](http://en.wikipedia.org/wiki/Conditional_comment) supported by Internet Explorer browsers for just this sort of situation. It’s a good thing, too, because it means we can include the HTML5 shim only for IE browsers less than version 9, leaving other browsers such as Firefox, Chrome, and Safari unaffected.

The next section includes a **header** for the site’s (plain-text) logo, a couple of divisions (using the **div** tag), and a list of elements with navigation links:

	<header class="navbar navbar-fixed-top navbar-inverse">
	  <div class="navbar-inner">
	    <div class="container">
	      <%= link_to "sample app", '#', id: "logo" %>
	      <nav>
	        <ul class="nav pull-right">
	          <li><%= link_to "Home",    '#' %></li>
	          <li><%= link_to "Help",    '#' %></li>
	          <li><%= link_to "Sign in", '#' %></li>
	        </ul>
	      </nav>
	    </div>
	  </div>
	</header>

Here the **header** tag indicates elements that should go at the top of the page. We’ve given the header tag three CSS classes, called **navbar**, **navbar-fixed-top**, and **navbar-inverse**, separated by spaces:

	<header class="navbar navbar-fixed-top navbar-inverse">

All HTML elements can be assigned both classes and ids; these are merely labels, and are useful for styling with CSS (Section 5.1.2). The main difference between **classes** and **ids** is that classes can be used multiple times on a page, but ids can be used only once. In the present case, all the **navbar** classes have special meaning to the *Bootstrap framework*, which we’ll install and use in Section 5.1.2.

Inside the **header** tag, we see a couple of **div** tags:

	<div class="navbar-inner">
	  <div class="container">

The **div** tag is a generic division; it doesn’t do anything apart from *divide the document into distinct parts*. In older-style HTML, div tags are used for nearly all site divisions, but HTML5 adds the **header**, **nav**, and **section** elements for divisions common to many applications. In this case, each div has a CSS class as well. As with the **header** tag’s classes, these classes have special meaning to Bootstrap.

After the divs, we encounter some embedded Ruby:

	<%= link_to "sample app", '#', id: "logo" %>
	<nav>
	  <ul class="nav pull-right">
	    <li><%= link_to "Home",    '#' %></li>
	    <li><%= link_to "Help",    '#' %></li>
	    <li><%= link_to "Sign in", '#' %></li>
	  </ul>
	</nav>

This uses the Rails helper `link_to` to create links; the first argument to `link_to` is the link text, while the second is the URL. We’ll fill in the URLs with *named routes* in Section 5.3.3, but for now we use the stub URL **’#’** commonly used in web design.

The third argument is an options *hash*, in this case adding the CSS id logo to the sample app link. (The other three links have no options hash, which is fine since it’s optional.) Rails helpers often take options hashes in this way, giving us the flexibility to add arbitrary HTML options without ever leaving Rails.

The **nav** tag, though formally unnecessary here, communicates the purpose of the navigation links. The **nav** and **pull-right** classes on the **ul** tag have special meaning to Bootstrap.

The final part of the layout is a **div** for the main content:

	<div class="container">
	  <%= yield %>
	</div>

As before, the container class has special meaning to Bootstrap.

To take advantage of the upcoming style elements, we’ll add some extra elements to the **home.html.erb** view (Listing 5.2).

	Listing 5.2: The Home page with a link to the signup page.
	app/views/static_pages/home.html.erb
	 <div class="center hero-unit">
	  <h1>Welcome to the Sample App</h1>

	  <h2>
	    This is the home page for the
	    <a href="http://railstutorial.org/">Ruby on Rails Tutorial</a>
	    sample application.
	  </h2>

	  <%= link_to "Sign up now!", '#', class: "btn btn-large btn-primary" %>
	</div>

	<%= link_to image_tag("rails.png", alt: "Rails"), 'http://rubyonrails.org/' %>

In preparation for adding users to our site in Chapter 7, the first **link_to** creates a stub link of the form

	<%= link_to "Sign up now!", '#', class: "btn btn-large btn-primary" %>

In the **div** tag, the **hero-unit** CSS class has a special meaning to Bootstrap, as do the **btn**, **btn-large**, and **btn-primary** classes in the signup button.

The second `link_to` shows off the **image_tag** helper, which takes as arguments the path to an image and an optional options hash, in this case setting the **alt** attribute of the image tag using symbols. To make this clearer, let’s look at the HTML this tag produces:

	<%= link_to image_tag("rails.png", alt: "Rails"), 'http://rubyonrails.org/' %>
	<img alt="Rails" src="/assets/rails.png" />

(Note that the **src** attribute doesn’t include **images**; Rails automatically makes the association of the file with the **images** directory on the server. Placing all the assets in the same **assets** directory allows them to be served faster.) The **alt** attribute is what will be displayed if there is no image, and it is also what will be displayed by screen readers for the visually impaired. Although people are sometimes sloppy about including the alt attribute for images, it is in fact required by the HTML standard. Luckily, Rails includes a default **alt** attribute; if you don’t specify the attribute in the call to **image_tag**, Rails just uses the image filename (minus extension).

In previous versions of Rails, the *rails.png* logo was included automatically with every Rails project, but in the latest version it doesn’t get generated as part of rails new, so you should download it from the main Ruby on Rails page at **http://rubyonrails.org/images/rails.png** and place it in the **app/assets/images/** directory. (You may also have to create that directory as well, either with **mkdir** or with a graphical file manager.) Because we used the **image_tag** helper in Listing 5.2, Rails will automatically find any images in that directory using the asset pipeline (Section 5.2).

<figure>
  <figcaption style="text-align:center;">Figure 5.2: The Home page (/static_pages/home) with no custom CSS.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/layout_no_logo_or_custom_css_bootstrap_rails_4.png" alt="home" title="home">
</figure>

## 5.1.2 - Bootstrap and custom CSS
In Section 5.1.1, *we associated many of the HTML elements with CSS classes*, which gives us considerable flexibility in constructing a layout based on CSS. As noted in Section 5.1.1, many of these classes are specific to Bootstrap, a framework from Twitter that makes it easy to add nice web design and user interface elements to an HTML5 application. In this section, we’ll *combine Bootstrap with some custom CSS rules* to start adding some style to the sample application.

Our first step is to add *Bootstrap*, which in Rails applications can be accomplished with the **bootstrap-sass** gem, as shown in Listing 5.3. (To fix a version incompatibility, Listing 5.3 also fixes the version of *Sprockets*, part of the asset pipeline covered in Section 5.2.) The Bootstrap framework natively uses the [LESS CSS](http://lesscss.org/) language for making dynamic stylesheets, but the Rails asset pipeline supports the (very similar) [Sass](http://sass-lang.com/) language by default (Section 5.2), so **bootstrap-sass** converts LESS to Sass and makes all the necessary Bootstrap files available to the current application.

	Listing 5.3: Adding the bootstrap-sass gem to the Gemfile.
	gem 'bootstrap-sass', '2.3.2.0'
	gem 'sprockets', '2.11.0'

To install Bootstrap, we run **bundle install** as usual:

	$ bundle install

Then restart the web server to incorporate the changes into the development application. Finally, as of Rails 4.0 we need to add a line to **config/application.rb** to make **bootstrap-sass** compatible with the asset pipeline, as shown in Listing 5.4.

	Listing 5.4: Adding a line for asset pipeline compatibility.
	config/application.rb
	 require File.expand_path('../boot', __FILE__)
	.
	.
	.
	module SampleApp
	  class Application < Rails::Application
	    .
	    .
	    .
	    config.assets.precompile += %w(*.png *.jpg *.jpeg *.gif)
	  end
	end

The first step in adding custom CSS to our application is to open a file to contain it:

	$ subl app/assets/stylesheets/custom.css.scss

Here both the directory name and filename are important. The directory

	app/assets/stylesheets

is part of the asset pipeline (Section 5.2), and any stylesheets in this directory will automatically be included as part of the **application.css** file included in the site layout. Furthermore, the filename **custom.css.scss** includes the **.css** extension, which indicates a CSS file, and the **.scss** extension, which indicates a “*Sassy CSS*” file and arranges for the asset pipeline to process the file using *Sass*. (We won’t be using Sass until Section 5.2.2, but it’s needed now for the *bootstrap-sass* gem to work its magic.)

Inside the file for custom CSS, we can use the **@import** function to include Bootstrap, as shown in Listing 5.5.

	Listing 5.5: Adding Bootstrap CSS.
	app/assets/stylesheets/custom.css.scss
	@import "bootstrap";

This one line includes the entire Bootstrap CSS framework, with the result shown in in Figure 5.3. (You may have to use *Ctrl-C* to restart the local web server. It’s also worth noting that the screenshots use Bootstrap 2.0, whereas the tutorial currently uses Bootstrap 2.3, so there may be minor differences in appearance. These are not cause for concern.) The placement of the text isn’t good and the logo doesn’t have any style, but the colors and signup button look promising.

<figure>
  <figcaption style="text-align:center;">Figure 5.3: The sample application with Bootstrap CSS.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/sample_app_only_bootstrap_4_0.png" alt="home" title="home">
</figure>

Next we’ll add some CSS that will be used site-wide for styling the layout and each individual page, as shown in Listing 5.6. There are quite a few rules in Listing 5.6; to get a sense of what a CSS rule does, it’s often helpful to comment it out using CSS comments, i.e., by putting it inside **/* … */**, and seeing what changes. The result of the CSS in Listing 5.6 is shown in Figure 5.4.

	Listing 5.6: Adding CSS for some universal styling applying to all pages.
	app/assets/stylesheets/custom.css.scss
	 @import "bootstrap";

	/* universal */

	html {
	  overflow-y: scroll;
	}

	body {
	  padding-top: 60px;
	}

	section {
	  overflow: auto;
	}

	textarea {
	  resize: vertical;
	}

	.center {
	  text-align: center;
	}

	.center h1 {
	  margin-bottom: 10px;
	}

<figure>
  <figcaption style="text-align:center;">Figure 5.4: Adding some spacing and other universal styling.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/sample_app_universal_4_0.png" alt="home" title="home">
</figure>

Although Bootstrap comes with CSS rules for nice typography, we’ll also add some custom rules for the appearance of the text on our site, as shown in Listing 5.7.

	Listing 5.7: Adding CSS for nice typography.
	app/assets/stylesheets/custom.css.scss
	 @import "bootstrap";
	.
	.
	.

	/* typography */

	h1, h2, h3, h4, h5, h6 {
	  line-height: 1;
	}

	h1 {
	  font-size: 3em;
	  letter-spacing: -2px;
	  margin-bottom: 30px;
	  text-align: center;
	}

	h2 {
	  font-size: 1.2em;
	  letter-spacing: -1px;
	  margin-bottom: 30px;
	  text-align: center;
	  font-weight: normal;
	  color: #999;
	}

	p {
	  font-size: 1.1em;
	  line-height: 1.7em;
	}

<figure>
  <figcaption style="text-align:center;">Figure 5.5: Adding some typographic styling.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/sample_app_typography_4_0.png" alt="home" title="home">
</figure>

Finally, we’ll add some rules to style the *site’s logo*, which simply consists of the text “sample app”. The CSS in Listing 5.8 converts the text to uppercase and modifies its size, color, and placement. (We’ve used a CSS id because we expect the site logo to appear on the page only once, but you could use a class instead.)

	Listing 5.8: Adding CSS for the site logo.
	app/assets/stylesheets/custom.css.scss
	 @import "bootstrap";
	.
	.
	.

	/* header */

	#logo {
	  float: left;
	  margin-right: 10px;
	  font-size: 1.7em;
	  color: #fff;
	  text-transform: uppercase;
	  letter-spacing: -1px;
	  padding-top: 9px;
	  font-weight: bold;
	  line-height: 1;
	}

	#logo:hover {
	  color: #fff;
	  text-decoration: none;
	}

<figure>
  <figcaption style="text-align:center;">Figure 5.6: The sample app with nicely styled logo.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/sample_app_logo_4_0.png" alt="home" title="home">
</figure>

## 5.1.3 - Partials
Although the layout in Listing 5.1 serves its purpose, it’s getting a little *cluttered*. The HTML shim takes up three lines and uses weird IE-specific syntax, so it would be nice to tuck it away somewhere on its own. In addition, the header HTML forms a logical unit, so it should all be packaged up in one place. The way to achieve this in Rails is to use a facility called **partials**. Let’s first take a look at what the layout looks like after the partials are defined (Listing 5.9).

	Listing 5.9: The site layout with partials for the stylesheets and header.
	app/views/layouts/application.html.erb
	 <!DOCTYPE html>
	<html>
	  <head>
	    <title><%= full_title(yield(:title)) %></title>
	    <%= stylesheet_link_tag "application", media: "all",
	                                           "data-turbolinks-track" => true %>
	    <%= javascript_include_tag "application", "data-turbolinks-track" => true %>
	    <%= csrf_meta_tags %>
	    <%= render 'layouts/shim' %>
	  </head>
	  <body>
	    <%= render 'layouts/header' %>
	    <div class="container">
	      <%= yield %>
	    </div>
	  </body>
	</html>

In Listing 5.9, we’ve replaced the HTML shim stylesheet lines with a single call to a Rails **helper** called **render**:

	<%= render 'layouts/shim' %>


The effect of this line is to look for a file called **app/views/layouts/_shim.html.erb**, evaluate its contents, and insert the results into the view. Note the leading underscore on the filename `_shim.html.erb`; this underscore is the universal convention for naming partials, and among other things makes it possible to identify all the partials in a directory at a glance.

Of course, to get the partial to work, we have to fill it with some content; in the case of the shim partial, this is just the three lines of shim code from Listing 5.1; the result appears in Listing 5.10.

	Listing 5.10: A partial for the HTML shim.
	app/views/layouts/_shim.html.erb
	 <!--[if lt IE 9]>
	<script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
	<![endif]-->

Similarly, we can move the header material into the partial shown in Listing 5.11 and insert it into the layout with another call to **render**.

	Listing 5.11: A partial for the site header.
	app/views/layouts/_header.html.erb
	 <header class="navbar navbar-fixed-top navbar-inverse">
	  <div class="navbar-inner">
	    <div class="container">
	      <%= link_to "sample app", '#', id: "logo" %>
	      <nav>
	        <ul class="nav pull-right">
	          <li><%= link_to "Home",    '#' %></li>
	          <li><%= link_to "Help",    '#' %></li>
	          <li><%= link_to "Sign in", '#' %></li>
	        </ul>
	      </nav>
	    </div>
	  </div>
	</header>

Now that we know how to make partials, let’s add a site footer to go along with the header. By now you can probably guess that we’ll call it **_footer.html.erb** and put it in the layouts directory (Listing 5.12).

	Listing 5.12: A partial for the site footer.
	app/views/layouts/_footer.html.erb
	 <footer class="footer">
	  <small>
	    <a href="http://railstutorial.org/">Rails Tutorial</a>
	    by Michael Hartl
	  </small>
	  <nav>
	    <ul>
	      <li><%= link_to "About",   '#' %></li>
	      <li><%= link_to "Contact", '#' %></li>
	      <li><a href="http://news.railstutorial.org/">News</a></li>
	    </ul>
	  </nav>
	</footer>

We can render the footer partial in the layout by following the same pattern as the stylesheets and header partials (Listing 5.13).

	Listing 5.13: The site layout with a footer partial.
	app/views/layouts/application.html.erb
	 <!DOCTYPE html>
	<html>
	  <head>
	    <title><%= full_title(yield(:title)) %></title>
	    <%= stylesheet_link_tag "application", media: "all",
	                                           "data-turbolinks-track" => true %>
	    <%= javascript_include_tag "application", "data-turbolinks-track" => true %>
	    <%= csrf_meta_tags %>
	    <%= render 'layouts/shim' %>
	  </head>
	  <body>
	    <%= render 'layouts/header' %>
	    <div class="container">
	      <%= yield %>
	      <%= render 'layouts/footer' %>
	    </div>
	  </body>
	</html>

Of course, the footer will be ugly without some styling (Listing 5.14).

	Listing 5.14: Adding the CSS for the site footer.
	app/assets/stylesheets/custom.css.scss
	 .
	.
	.

	/* footer */

	footer {
	  margin-top: 45px;
	  padding-top: 5px;
	  border-top: 1px solid #eaeaea;
	  color: #999;
	}

	footer a {
	  color: #555;
	}

	footer a:hover {
	  color: #222;
	}

	footer small {
	  float: left;
	}

	footer ul {
	  float: right;
	  list-style: none;
	}

	footer ul li {
	  float: left;
	  margin-left: 10px;
	}

<figure>
  <figcaption style="text-align:center;">Figure 5.7: The Home page (/static_pages/home) with an added footer.</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="railsFigures/site_with_footer_bootstrap_4_0.png" alt="footer" title="footer">
</figure>

# 5.2 - Sass and the asset pipeline
One of the *most notable additions* in recent versions of Rails is the **asset pipeline**, which significantly improves the production and management of static assets such as *CSS, JavaScript, and images*. This section gives a high-level overview of the asset pipeline and then shows how to use a remarkable tool for making CSS called Sass, now included by default as part of the asset pipeline.

## 5.2.1 - The asset pipeline
**Asset directories**

In versions of Rails before 3.0 (including 3.0 itself), static assets lived in the **public/** directory, as follows:

- **public/stylesheets**
- **public/javascripts**
- **public/images**

Files in these directories are (even post-3.0) automatically served up via requests to **http://example.com/stylesheets**, etc.

Starting in Rails 3.1, and continuing in Rails 4, there are *three canonical directories for static assets*, each with its own purpose:

- **app/assets**: assets specific to the present application
- **lib/assets**: assets for libraries written by your dev team
- **vendor/assets**: assets from third-party vendors

**Manifest files**

Once you’ve placed your assets in their logical locations, you can use *manifest files* to tell Rails (via the [Sprockets](https://github.com/sstephenson/sprockets) gem) how to combine them to form single files. (This applies to *CSS and JavaScript* but not to images.) As an example, let’s take a look at the default manifest file for app stylesheets (Listing 5.15).

	Listing 5.15: The manifest file for app-specific CSS.
	app/assets/stylesheets/application.css
	 /*
	 * This is a manifest file that'll automatically include all the stylesheets
	 * available in this directory and any sub-directories. You're free to add
	 * application-wide styles to this file and they'll appear at the top of the
	 * compiled file, but it's generally better to create a new file per style
	 * scope.
	 *= require_self
	 *= require_tree .
	*/

The key lines here are actually CSS comments, but they are used by Sprockets to include the proper files:

	/*
	 .
	 .
	 .
	 *= require_self
	 *= require_tree .
	*/

Here

	*= require_tree .

ensures that all CSS files in the **app/assets/stylesheets** directory (including the tree subdirectories) are included into the application CSS. The line

	*= require_self

specifies where in the loading sequence the CSS in application.css itself gets included.

**Preprocessor engines**

After you’ve assembled your assets, Rails prepares them for the site template by running them through several preprocessing engines and using the manifest files to combine them for delivery to the browser.

We tell Rails which processor to use using filename extensions; the three most common cases are **.scss** for Sass, **.coffee** for CoffeeScript, and **.erb** for embedded Ruby (ERb).

We first covered ERb in Section 3.3.3, and cover Sass in Section 5.2.2. We won’t be needing CoffeeScript in this tutorial, but it’s an elegant little language that compiles to JavaScript. ([The RailsCast on CoffeeScript basics](http://railscasts.com/episodes/267-coffeescript-basics) is a good place to start.)

The preprocessor engines can be chained, so that

**foobar.js.coffee**

gets run through the CoffeeScript processor, and

**foobar.js.erb.coffee**

gets run through both CoffeeScript and ERb (with the code running from *right to left*, i.e., CoffeeScript first).

**Efficiency in production**

One of the best things about the asset pipeline is that it automatically results in assets that are optimized to be efficient in a production application.

Traditional methods for organizing CSS and JavaScript involve splitting functionality into separate files and using nice formatting (with lots of indentation). While convenient for the programmer, this is inefficient in production; including multiple full-sized files can significantly slow page-load times (one of the most important factors affecting the quality of the user experience).

With the asset pipeline, in production all the application stylesheets get rolled into one CSS file (**application.css**), all the application JavaScript code gets rolled into one JavaScript file (**javascripts.js**), and all such files (including those in **lib/assets** and **vendor/assets**) are minified to remove the unnecessary whitespace that bloats file size.

As a result, we get the best of both worlds: multiple nicely formatted files for programmer convenience, with single optimized files in production.

## 5.2.2 - Syntactically awesome stylesheets
*Sass* is a language for writing stylesheets that improves on CSS in many ways. In this section, we cover two of the most important improvements, *nesting* and *variables*. (A third technique, *mixins*, is introduced in Section 7.1.1.)

As noted briefly in Section 5.1.2, Sass supports a format called *SCSS* (indicated with a **.scss** filename extension), which is a *strict superset of CSS itself*; that is, *SCSS only adds features to CSS*, rather than defining an entirely new syntax. This means that *every valid CSS file is also a valid SCSS file*, which is convenient for projects with existing style rules. In our case, we used SCSS from the start in order to take advantage of Bootstrap. Since the Rails asset pipeline automatically uses Sass to process files with the **.scss** extension, the **custom.css.scss** file will be run through the Sass preprocessor before being packaged up for delivery to the browser.

**Nesting**

A common pattern in stylesheets is having rules that apply to nested elements. For example, in Listing 5.6 we have rules both for **.center** and for **.center h1**:

	.center {
	  text-align: center;
	}

	.center h1 {
	  margin-bottom: 10px;
	}

We can replace this in Sass with

	.center {
	  text-align: center;
	  h1 {
	    margin-bottom: 10px;
	  }
	}

There’s a *second candidate* for nesting that requires a slightly different syntax. In Listing 5.8, we have the code

	#logo {
	  float: left;
	  margin-right: 10px;
	  font-size: 1.7em;
	  color: #fff;
	  text-transform: uppercase;
	  letter-spacing: -1px;
	  padding-top: 9px;
	  font-weight: bold;
	  line-height: 1;
	}

	#logo:hover {
	  color: #fff;
	  text-decoration: none;
	}

Here the logo id **#logo** appears twice, once by itself and once with the hover attribute (which controls its appearance when the mouse pointer hovers over the element in question). In order to nest the second rule, we need to reference the parent element **#logo**; in SCSS, this is accomplished with the ampersand character `&` as follows:

	#logo {
	  float: left;
	  margin-right: 10px;
	  font-size: 1.7em;
	  color: #fff;
	  text-transform: uppercase;
	  letter-spacing: -1px;
	  padding-top: 9px;
	  font-weight: bold;
	  line-height: 1;
	  &:hover {
	    color: #fff;
	    text-decoration: none;
	  }
	}

Sass allows us to define variables to eliminate duplication and write more expressive code. For example, looking at Listing 5.7 and Listing 5.14, we see that there are repeated references to the same color:

	h2 {
	  .
	  .
	  .
	  color: #999;
	}
	.
	.
	.
	footer {
	  .
	  .
	  .
	  color: #999;
	}

In this case, #999 is a light gray, and we can give it a name by defining a variable as follows:

	$lightGray: #999;
	.
	.
	.
	h2 {
	  .
	  .
	  .
	  color: $lightGray;
	}
	.
	.
	.
	footer {
	  .
	  .
	  .
	  color: $lightGray;
	}

Because variable names such as **$lightGray** are more descriptive than **#999**, it’s often useful to define variables even for values that aren't repeated. Indeed, the Bootstrap framework defines a large number of variables for colors, available online on the [Bootstrap page of LESS variables](http://bootstrapdocs.com/v2.0.4/docs/less.html). That page defines variables using LESS, not Sass, but the **bootstrap-sass** gem provides the Sass equivalents. It is not difficult to guess the correspondence; where LESS uses an "at" sign `@`, Sass uses a dollar sign `$`. Looking the Bootstrap variable page, we see that there is a variable for light gray:

This means that, via the bootstrap-sass gem, there should be a corresponding SCSS variable **$grayLight**. We can use this to replace our custom variable, **$lightGray**, which gives

	h2 {
	  .
	  .
	  .
	  color: $grayLight;
	}
	.
	.
	.
	footer {
	  .
	  .
	  .
	  color: $grayLight;
	}

# 5.3 - Layout links
Now that we've finished a site layout with decent styling, it’s time to start filling in the links we’ve stubbed out with **’#’**. Of course, we could hard-code links like

	<a href="/static_pages/about">About</a>

but that isn’t the Rails Way. For one, it would be nice if the URL for the about page were **/about** rather than **/static_pages/about**. Moreover, Rails conventionally uses *named routes*, which involves code like

	<%= link_to "About", about_path %>

This way the code has a more **transparent** meaning, and it’s also more **flexible** since we can change the definition of `about_path` and have the URL change everywhere `about_path` is used.

The full list of our planned links appears in Table 5.1, along with their mapping to URLs and routes. We’ll implement all but the last one by the end of this chapter. (We’ll make the last one in Chapter 8.)

Page |	URL |	Named route
-|-|-
Home |	/ |	root_path
About |	/about |	about_path
Help |	/help |	help_path
Contact |	/contact |	contact_path
Sign up |	/signup |	signup_path
Sign in	| /signin |	signin_path

## 5.3.1 - Route tests
With the work we’ve done writing integration tests for the static pages, writing tests for the routes is simple: we just replace each occurrence of a hard-coded address with the desired named route from Table 5.1. In other words, we change

	visit '/static_pages/about'

to

	visit about_path

## 5.3.2 - Rails routes
Now that we have tests for the URLs we want, it’s time to get them to work. As noted in Section 3.1, the file Rails uses for URL mappings is **config/routes.rb**. If you take a look at the default routes file, you’ll see that it’s quite a mess, but it’s a useful mess—full of commented-out example route mappings. I suggest reading through it at some point, and I also suggest taking a look at the [Rails Guides article “Rails Routing from the outside in”](http://guides.rubyonrails.org/routing.html) for a much more in-depth treatment of routes.

To define the named routes, we need to replace rules such as

	get 'static_pages/help'

with

	match '/help', to: 'static_pages#help', via: 'get'

This arranges both for a valid page at **/help** (responding to GET requests) and a named route called **help_path** that returns the path to that page. (Actually, using **get** in place of **match** gives the same named routes, but using **match** is more conventional.)

In addition, as mentioned above, the code **match ’/about’** also automatically creates *named routes* for use in the controllers and views:

	about_path -> '/about'
	about_url  -> 'http://localhost:3000/about'

Applying this pattern to the other static pages gives Listing 5.24. The only exception is the Home page, which we’ll take care of in Listing 5.26.

	Listing 5.24: Routes for static pages.
	config/routes.rb
	 SampleApp::Application.routes.draw do
	  match '/help',    to: 'static_pages#help',    via: 'get'
	  match '/about',   to: 'static_pages#about',   via: 'get'
	  match '/contact', to: 'static_pages#contact', via: 'get'
	  .
	  .
	  .
	end

With these routes now defined, the tests for the Help, About, and Contact pages should pass:

	if you run spork, you should restart it
	$ bundle exec rspec spec/requests/static_pages_spec.rb

This leaves the test for the Home page as the last one to fail.

To establish the route mapping for the Home page, we could use code like this:

	root  'static_pages#home'

	Listing 5.26: Adding a mapping for the root route.
	config/routes.rb
	 SampleApp::Application.routes.draw do
	  root  'static_pages#home'
	  match '/help',    to: 'static_pages#help',    via: 'get'
	  match '/about',   to: 'static_pages#about',   via: 'get'
	  match '/contact', to: 'static_pages#contact', via: 'get'
	  .
	  .
	  .
	end

With that, all of the routes for static pages are working, and the tests should pass:

	if you run spork, you should restart it
	$ bundle exec rspec spec/requests/static_pages_spec.rb

Now we just have to fill in the links in the layout.

## 5.3.3 - Named routes
Let’s put the named routes created in Section 5.3.2 to work in our layout. This will entail filling in the second arguments of the **link_to** functions with the proper named routes. For example, we’ll convert

	<%= link_to "About", '#' %>

to

	<%= link_to "About", about_path %>

and so on.

We’ll start in the header partial, **_header.html.erb**, which has links to the Home and Help pages. While we’re at it, we’ll follow a common web convention and link the logo to the Home page as well. We won’t have a named route for the “Sign in” link until Chapter 8, so we’ve left it as **’#’** for now.

The other place with links is the footer partial, **_footer.html.erb**, which has links for the About and Contact pages.

## 5.3.4 - Pretty RSpec
We noted in Section 5.3.1 that the tests for the static pages are getting a little *verbose* and *repetitive* (Listing 5.23). In this section we’ll make use of the latest features of RSpec to make our tests more *compact* and *elegant*.

	Listing 5.30: Prettier tests for the static pages.
	spec/requests/static_pages_spec.rb
	require 'spec_helper'

	describe "Static pages" do

	  subject { page }

	  describe "Home page" do
	    before { visit root_path }

	    it { should have_content('Sample App') }
	    it { should have_title(full_title('')) }
	    it { should_not have_title('| Home') }
	  end

	  describe "Help page" do
	    before { visit help_path }

	    it { should have_content('Help') }
	    it { should have_title(full_title('Help')) }
	  end

	  describe "About page" do
	    before { visit about_path }

	    it { should have_content('About') }
	    it { should have_title(full_title('About Us')) }
	  end

	  describe "Contact page" do
	    before { visit contact_path }

	    it { should have_content('Contact') }
	    it { should have_title(full_title('Contact')) }
	  end
	end

# 5.4 - User signup: A first step
As a *capstone* to our work on the layout and routing, in this section we’ll *make a route for the signup page*, which will mean *creating a second controller along the way*. This is a first important step toward allowing users to register for our site; we’ll take the next step, *modeling users*, in Chapter 6, and we’ll finish the job in Chapter 7.

## 5.4.1 - Users controller
It’s been a while since we created our first controller, the StaticPages controller, way back in Section 3.1. It’s time to create a second one, the *Users controller*. As before, we’ll use **generate** to make the simplest controller that meets our present needs, namely, one with a stub signup page for new users. Following the conventional REST architecture favored by Rails, we’ll call the action for new users **new** and pass it as an argument to **generate controller** to create it automatically (Listing 5.31).

	Listing 5.31: Generating a Users controller (with a new action).
	$ rails generate controller Users new --no-test-framework

## 5.4.2 - Signup URL
Write an integration test

	$ rails generate integration_test user_pages

Test for signup page

	Listing 5.34: The initial spec for users, with a test for the signup page.
	spec/requests/user_pages_spec.rb
	 require 'spec_helper'

	describe "User pages" do

	  subject { page }

	  describe "signup page" do
	    before { visit signup_path }

	    it { should have_content('Sign up') }
	    it { should have_title(full_title('Sign up')) }
	  end
	end

route file

	match '/signup', to: 'users#new', via: :get

# 5.5 - Conclusion
In this chapter, we’ve *hammered our application layout into shape and polished up the routes*. The rest of the book is dedicated to fleshing out the sample application: first, by *adding users who can sign up, sign in, and sign out*; next, by *adding user microposts*; and, finally, by *adding the ability to follow other users*.

At this point, if you are using Git you should merge the changes back into the master branch:

	$ git add .
	$ git commit -m "Finish layout and routes"
	$ git checkout master
	$ git merge filling-in-layout

You can also push up to GitHub:

	$ git push

Finally, you can deploy to Heroku:

	$ git push heroku

The result should be a working sample application on the production server:

	$ heroku open

If you run into trouble, try running

	$ heroku logs

to debug the error using the Heroku logfile.

# 5.6 - Exercises
