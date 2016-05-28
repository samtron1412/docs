[TOC]

# Overview
Web Development

# [Layers of the full stack developer](http://www.laurencegellert.com/2012/08/what-is-a-full-stack-developer/)

## 1. Server, Network, and Hosting Environment.
A) This involves understanding what can break and why, taking no resource for granted.
B) Appropriate use of the file system, cloud storage, network resources, and an understanding of data redundancy and availability is necessary.
C) How does the application scale given the hardware constraints?
D) What about multi-threading and race conditions? Guess what, you won’t see those on your development machine, but they can and do happen in the real world.
E) Full stack developers can work side by side with DevOps. The system should provide useful error messages and logging capabilities. DevOps will see the messages before you will, so make them count.

## 2. Data Modeling
A) If the data model is flawed, the business logic and higher layers start to need strange (ugly) code to compensate for corner cases the data model doesn’t cover.
B) Full stack developers know how to create a reasonably normalized relational model, complete with foreign keys, indexes, views, lookup tables, etc.
C) Full stack developers are familiar with the concept of non-relational data stores and understand where they shine over relational data stores.

## 3. Business Logic
A) The heart of the value the application provides.
B) Solid object oriented skills are needed here.
C) Frameworks might be needed here as well.

## 4. API layer / Action Layer / MVC
A) How the outside world operates against the business logic and data model.
B) Frameworks at this level should be used heavily.
C) Full stack developers have the ability to write clear, consistent, simple to use interfaces. The heights to which some APIs are convoluted repel me.

## 5. User Interface
A) Full stack developers: a) understand how to create a readable layout, or b) acknowledge they need help from artists and graphic designers. Either way, implementing a good visual design is key.
B) Can include mastery of HTML5 / CSS.
C) JavaScript is the up and coming language of the future and lots of exciting work is being done in the JavaScript world (node, backbone, knockout…)

## 6. User Experience
A) Full stack developers appreciate that users just want things to work.
B) A good system doesn’t give its users carpal tunnel syndrome or sore eyes. A full stack developer can step back and look at a process that needs 8 clicks and 3 steps, and get it down to one click.
C) Full stack developers write useful error messages. If something breaks, be apologetic about it. Sometimes programmers inadvertently write error messages that can make people feel stupid.

## 7. Understanding what the customer and the business need.
A) Now we are blurring into the line of architect, but that is too much of a hands off role.
B) Full stack developers have a grasp of what is going on in the field when the customer uses the software. They also have a grasp of the business.

## Other Pieces of the Puzzle:
1. Ability to write quality unit tests. By the way, even JavaScript can have unit tests these days.
2. Understanding of repeatable automated processes for building the application, testing it, documenting it, and deploying it at scale.
3. An awareness of security concerns is important, as each layer presents its own possible vulnerabilities.

# Tools
[Firebug vs Firefox Deveoper Tools](http://stackoverflow.com/questions/19180494/what-unique-features-does-firebug-have-that-are-not-built-in-to-firefox):
- Has `DOM` panel, native tool has no
- Has `Cookies` panel
- Firebug submenus for Net, CSS, and HTML panels have filters unavailable in the native tool
- Native tool has built-in Profiler, Firebug needs YSlow

# Tutorial
## Analytics
- [Piwik](https://github.com/piwik/piwik)
- [Google Analytics](https://www.google.com/analytics/)
- [Clicky](https://www.clicky.com)

## Font
- [Google Fonts](https://www.google.com/fonts/): Open Sans
- [Font Awesome](https://github.com/FortAwesome/Font-Awesome): useful icons

## [Favicon](https://en.wikipedia.org/wiki/Favicon)
	<link rel="shortcut icon" href="http://example.com/myicon.ico" />
	<link rel="icon" type="image/png" href="http://example.com/image.png" />

## Setup mail server
- [mail in the box](https://github.com/mail-in-a-box/mailinabox)
- [set up windows mail server](http://inchoo.net/magento/installation-and-configuration-of-local-mail-server-for-windows-hmail-server/)
	+ https://gist.github.com/samtron1412/526e1e054d4e78fd5ee1
- [dummy mail server](https://github.com/Nilhcem/FakeSMTP)
- [send email via Gmail SMTP](http://www.mkyong.com/java/javamail-api-sending-email-via-gmail-smtp-example/)

## [Make social network button](http://blog.hubspot.com/blog/tabid/6307/bid/29544/The-Ultimate-Cheat-Sheet-for-Creating-Social-Media-Buttons.aspx)

## HTTPS load resources
Change link from `http://something.com/...` to `//something.com/...` it will automatically use right protocol to load resources.

## [Run PHP Applications under CGI with Apache on CentOS 6](https://www.linode.com/docs/websites/apache/run-php-applications-under-cgi-with-apache-on-centos-6)

# [Static Site Generator](https://staticsitegenerators.net/)
- [StaticGen](https://www.staticgen.com/)
- [Rise of Static Site Generator](https://justinmayer.com/talks/static-site-generators/#/)

# Standards
## [Any browser](http://www.anybrowser.org/campaign/)

## [W3C validator](https://validator.w3.org/)

# Tips & Tricks
## [Source code comment styling tips](http://www.hongkiat.com/blog/source-code-comment-styling-tips/)
