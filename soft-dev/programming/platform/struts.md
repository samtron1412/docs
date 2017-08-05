[TOC]

# Overview
The Apache Struts web framework is a free open-source solution for creating Java web applications.

Elegant, extensible web framework for building enterprise-ready Java web applications based on MVC design pattern.

The framework provides three key components:
1. A "request" handler provided by the application developer that is mapped to a standard URI.
2. A "response" handler that transfers control to another resource which completes the response.
3. A tag library that helps developers create interactive form-based applications with server pages.

# Features
- POJO forms and POJO actions - you can use any POJO to receive the form input. Now you can see any POJO as an Action class.
- Tag support - form tags and the new tags
- AJAX support
- Easy integration - Spring, Tiles
- Template support - generating views using templates.
- Plugin support
- Profiling - to debug and profile the application.
- Easy to modify tags
- Promote less configuration
- View technologies

# Struts 2 Architecture
- Actions
- Interceptors
- Value Stack/OGNL
- Results / Result types
- View technologies

<figure>
  <figcaption style="text-align:center;">Struts 2 Architecture</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="struts2/struts_2_architecture.gif" alt="Struts2" title="Struts2">
</figure>

<figure>
  <figcaption style="text-align:center;">Struts 2 Architecture</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="struts2/Struts2-Architecture.png" alt="Struts2" title="Struts2">
</figure>

>Struts 2 is slightly different from a traditional MVC framework when the action takes role of the model rather than the controller.

# Key Technologies
## Request life cycle:
The user's request life cycle in Struts 2 as follows:
- User sends a request to the server for requesting for some resource (i.e pages).
- The **FilterDispatcher** looks at the request and then determines the appropriate Action.
- **Configured interceptors functionalities applies** such as validation, file upload etc.
- Selected action is executed to perform the requested operation.
- Again, *configured interceptors are applied to do any post-processing* if required.
- Finally the result is prepared by the view and returns the result to the user.

As you learnt from the Struts 2 architecture, when you click on a hyperlink or submit an HTML form in a Struts 2 web application, the input is collected by the Controller which is sent to a Java class called Actions. After the Action is executed, a Result selects a resource to render the response. The resource is generally a JSP, but it can also be a PDF file, an Excel spreadsheet, or a Java applet window.

| SN | Components & Description                                                                                                 |
| -  | -                                                                                                                        |
| 1  | Action: contain complete business logic and control the interaction between the use, the model, and the view.            |
| 2  | Interceptors: create if required or use existing interceptors. This is part of Controller                                |
| 3  | View: create a JSPs to interact with the user to take input and to present the final messages.                           |
| 4  | Configuration Files: to couple the Action, View and Controllers. These files are struts.xml, web.xml, struts.properties. |


# Struts 2
## Configuration
### web.xml
web.xml file which is an entry point for any request to Struts 2

The web.xml configuration file is a J2EE configuration file that determines how elements of the HTTP request are processed by the servlet container.

### struts.xml
configure like controller to binding model (action) with view.

	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE struts PUBLIC
	   "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
	   "http://struts.apache.org/dtds/struts-2.0.dtd">
	<struts>
	   <constant name="struts.devMode" value="true" />
	   <package name="helloworld" extends="struts-default">

	      <action name="hello"
	            class="com.tutorialspoint.struts2.HelloWorldAction"
	            method="execute">
	            <result name="success">/HelloWorld.jsp</result>
	      </action>
	      <-- more actions can be listed here -->

	   </package>
	   <-- more packages can be listed here -->

	</struts>

Package tag has the following attributes:

| Attribute      | Description                                                           |
| name(required) | The unique identifier for the package                                 |
| extends        | which package does this package extend from?                          |
| abstract       | If marked true, the package is not available for end user consumption |
| namespace      | Unique namespace for the actions                                      |




## Struts tag
The framework provides a tag library *decoupled from the view technology*. Most tags are supported in all template languages (see **JSP Tags**, Velocity Tags, and FreeMarker Tags), but some are currently only specific to one language. Whenever a tag doesn't have complete support for every language, it is noted on the tag's reference page.

Types of tags: generic and UI.

The tags are designed to display dynamic data.

Sometimes, we want to pass the dynamic data to a tag. The expression escape sequence is `%{...}`. Any text embedded in the escape sequence is evaluated as an expression.

The expression language ([OGNL](https://struts.apache.org/release/2.1.x/docs/ognl.html)) let us call methods and evaluate properties.

The value attribute is set automatically, whatever is passed to value is evaluated as an expression - NOT a String literal. For example, it will call getter of a property is passed to value. If we want pass a object like String, Integer, ... we use escape sequence `%{...}`. E.g, pass a String `%{'string'}`, pass an Integer `%{123}`.

### Note

	<s:iterator value="roleScreenDetailsList" status ="itemIndex">
	   <table>
	      <tr id="row_${itemIndex.count}">
	         <td><s:textfield name="roleDescription" id="Desc_%{#itemIndex.count}" /></td>
	      </tr>
	   </table>
	</s:iterator>

Always use expression `${}` instead of `<s:property />` (except for Type Conversion), see the Performance Tuning of Struts2.

Always use `OGNL` for attributes of Struts2 tag.

### [Generic Tags](https://struts.apache.org/release/2.1.x/docs/generic-tag-reference.html)
Used for controlling the execution flow when the pages render. Allow for data extraction from places other than your action or the value stack.
- Control Tags provide control flow, such as if, else, and iterator.
- Data Tags allow for data manipulation or creation, such as bean, push, and i18n.

#### [iterator](https://struts.apache.org/release/2.1.x/struts2-core/apidocs/org/apache/struts2/views/jsp/IteratorStatus.html)
The iterator tag can export an IteratorStatus object so that one can get information about the status of the iteration, such as:

- index: current iteration index, starts on 0 and increments in one on every iteration
- count: iterations so far, starts on 1. count is always index + 1
- first: true if index == 0
- even: true if (index + 1) % 2 == 0
- last: true if current iteration is the last iteration
- odd: true if (index + 1) % 2 == 1

Example

	<s:iterator status="status" value='%{0, 1}'>
		Index: <s:property value="%{#status.index}" /> <br />
		Count: <s:property value="%{#status.count}" /> <br />
	</s:iterator>

will print

      Index: 0
      Count: 1
      Index: 1
      Count: 2

#### [OGNL](https://struts.apache.org/release/2.1.x/docs/ognl.html)
sign (#)

#### [a](https://struts.apache.org/release/2.1.x/docs/a.html)


#### [url](https://struts.apache.org/release/2.1.x/docs/url.html)


#### [if](https://struts.apache.org/release/2.1.x/docs/if.html)


#### [sub set](https://struts.apache.org/release/2.1.x/docs/subset.html)



# Practice Knowledge
## ServletContext
http://www.mkyong.com/struts2/how-to-get-the-servletcontext-in-struts-2/
http://stackoverflow.com/questions/2797162/getresourceasstream-is-always-returning-null
http://stackoverflow.com/questions/3139532/nullpointerexception-when-reading-a-properties-file-in-java

## [Sending Email via Gmail SMTP server in JAVA](http://stackoverflow.com/questions/15597616/sending-email-via-gmail-smtp-server-in-java)
- [Sending email with TLS](http://stackoverflow.com/questions/411331/using-javamail-with-tls)
- [TLS/SSL](http://www.mkyong.com/java/javamail-api-sending-email-via-gmail-smtp-example/)



## Execute Action and methods
- When query URL to action, it default execute `execute` function in this action.
- When submit form from client to action by `input` tag in html, it will execute `method` function in properties `name="method:motorcycleBulkDelete"`
	+ `<input type="submit" id="motoNew_bikeBulkDeleteBtn" name="method:motorcycleBulkDelete" value="選択した車両を一括削除する">`

## Render JSP pages
- When method finish with `return "result_name"` it will render JSP specific with name `result_name`

```java
@Results({
    @Result(name="result_name", location="moto_new_input.jsp")}) //入力画面
```

## Action Chaining
- The framework provides the ability to chain multiple actions into a defined sequence or workflow.

```java
@Results({
    @Result(name="insert",type="chain",location="moto_list"), 	//車両一覧
    @Result(name="error", type="chain", location="top")}) //メニュー画面
```
