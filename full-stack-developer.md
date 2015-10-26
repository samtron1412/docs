[TOC]

# Overview
- http://www.laurencegellert.com/2012/08/what-is-a-full-stack-developer/

# Layers of the full stack
1. Server, Network, and Hosting Environment.
	A) This involves understanding what can break and why, taking no resource for granted.
	B) Appropriate use of the file system, cloud storage, network resources, and an understanding of data redundancy and availability is necessary.
	C) How does the application scale given the hardware constraints?
	D) What about multi-threading and race conditions? Guess what, you won’t see those on your development machine, but they can and do happen in the real world.
	E) Full stack developers can work side by side with DevOps. The system should provide useful error messages and logging capabilities. DevOps will see the messages before you will, so make them count.
2. Data Modeling
	A) If the data model is flawed, the business logic and higher layers start to need strange (ugly) code to compensate for corner cases the data model doesn’t cover.
	B) Full stack developers know how to create a reasonably normalized relational model, complete with foreign keys, indexes, views, lookup tables, etc.
	C) Full stack developers are familiar with the concept of non-relational data stores and understand where they shine over relational data stores.
3. Business Logic
	A) The heart of the value the application provides.
	B) Solid object oriented skills are needed here.
	C) Frameworks might be needed here as well.
4. API layer / Action Layer / MVC
	A) How the outside world operates against the business logic and data model.
	B) Frameworks at this level should be used heavily.
	C) Full stack developers have the ability to write clear, consistent, simple to use interfaces. The heights to which some APIs are convoluted repel me.
5. User Interface
	A) Full stack developers: a) understand how to create a readable layout, or b) acknowledge they need help from artists and graphic designers. Either way, implementing a good visual design is key.
	B) Can include mastery of HTML5 / CSS.
	C) JavaScript is the up and coming language of the future and lots of exciting work is being done in the JavaScript world (node, backbone, knockout…)
6. User Experience
	A) Full stack developers appreciate that users just want things to work.
	B) A good system doesn’t give its users carpal tunnel syndrome or sore eyes. A full stack developer can step back and look at a process that needs 8 clicks and 3 steps, and get it down to one click.
	C) Full stack developers write useful error messages. If something breaks, be apologetic about it. Sometimes programmers inadvertently write error messages that can make people feel stupid.
7. Understanding what the customer and the business need.
	A) Now we are blurring into the line of architect, but that is too much of a hands off role.
	B) Full stack developers have a grasp of what is going on in the field when the customer uses the software. They also have a grasp of the business.
 

Other Pieces of the Puzzle:

1. Ability to write quality unit tests. By the way, even JavaScript can have unit tests these days.
2. Understanding of repeatable automated processes for building the application, testing it, documenting it, and deploying it at scale.
3. An awareness of security concerns is important, as each layer presents its own possible vulnerabilities.