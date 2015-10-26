**Web application**: any application which resides on a server, and mainly used by human using web browser. All user interactivity is done through web pages.

**Web service**: server-based application (as above) which may be accessed over the web via HTTP, but is meant primarily for interaction with other programs. Generally it is WEB API for other applications.

---
**A web service**:

    Typically returns XML or JSON or something like that, something that is easily decoded by a program
    The results you get from a web service is typically not just shown to a person in its raw form (ie. since it isn't HTML, the results have to be reformatted, like placed into a form)
    The intended usage of a web service is that it is something an application can talk to

**A web application**

    Typically returns HTML or image data or similar
    The results you get from a web application is usually shown to a person, through a web browser

**As for similarities**:

    Both typically use HTTP(S) as the transport
    Both typically use HTTP authentication/authorization to secure data
    Both are typically hosted by a web server

So the main difference is who usually talks to them. A web service usually by another application, a web application usually by a web browser. Other than that they're pretty similar.

---
**Web application**: any application which resides on a server, but meant for use by humans, which uses web pages as the presentation layer. All user interactivity (the GUI) is done through web pages, but all data is stored and (mostly) manipulated on the server.

**Web service**: server-based application (as above) which may be accessed over the web via HTTP, but is meant primarily for interaction with other programs. Thus, it will have a clearly-defined API which consists of providing responses to HTTP GET and POST requests made by a remote application. Now, this doesn't mean you can't access a web service from your browser, but it means that the application won't necessarily have a GUI user interface. You will most likely, for example, receive all results of GET and POST requests as strings of XML, which requires a client-side parser.

---
**What is a web application?** web + application. A software application is something that is helping a user to achieve some specific goal, like MS Word, Calculator, Email Client etc. A web application, similarly, is an application which is available over a network or internet, it might be online banking application, some e-commerce application etc.

**What is a web service?** A service is similar to application in a sense that it is achieving a goal, but instead of being independent application, a service is providing inputs to some other application. For example, a service to add up two numbers, will take 2 numbers from a calculator app, add up two numbers, and return back to the calling applications.

Now how to take up the question if I should be creating a web application for a particular problem or web service. Let’s go back to calculator app, which needs a functionality to add 2 numbers. Web application approach will be to implement the add function inside the app, which is good enough if I know that this function is to be used only with this app. Web service approach will need the sum service to be independent of any application. This gives advantage that the same service can be used by multiple applications, this includes web apps, mobile apps or desktop apps as they will just need to connect to network and call the service to fulfill a requirement.
