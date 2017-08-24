[TOC]

# Overview
- Java framework to developing any Java application, there are extensions for building web application on top of the Java EE platform. Enabling a POJO based programming model.
- 

# Basic Ideas
Sử dụng một module quản lý các module khác. Dev chỉ cần liên hệ với module quản lý này để gọi các service.

## Dependency Injection flavor of IoC(Inversion of Control)
Một thiết kế quản lý các **module** theo chiều dọc, độc lập tương đối với nhau. Các module tách biệt với nhau, không liên quan đến nhau. Mỗi module có một file **interface** cung cấp các api để truy cập đến module đó và một file class hiện thực module đó.

Tăng tính **modularity** và **extensible** của chương trình. Được ứng dụng trong OOP(Object-oriented programming).

----
When writing a complex Java application, application classes should be as independent as possible of other Java classes to increase the possibility to reuse these classes and to test them independently of other classes while doing unit testing. DI helps in gluing these classes together and same time keeping them independent.

- **Dependency**: an association between two classes. E.g. class A is dependent on class B
- **Injection**: all this means is that class B will get injected into class A by the IoC.

DI can happen in the way of passing parameters to the constructor or by post-construction using setter methods.

### The Spring container is at the core of the Spring Framework
The container will create the objects, wire them together (boc chung lai), configure them, and manage their complete lifecycle from creation till destruction.

The Spring container uses dependency injection to manage the components that make up an application. These objects are called **Spring Beans**.

<figure>
  <figcaption style="text-align:center;">Spring IoC Container</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="spring/spring_ioc_container.jpg" alt="Spring" title="Spring">
</figure>


### Implementation techniques
#### Using [factory pattern](http://en.wikipedia.org/wiki/Factory_pattern)

#### Using a [service locator pattern](http://en.wikipedia.org/wiki/Service_locator_pattern)

#### Using a [dependency injection](http://en.wikipedia.org/wiki/Dependency_injection)
- A constructor injection
- A parameter injection
- A setter injection
- An interface injection

#### ...

## AOP (Aspect-oriented Programming)
A programming paradigm that aims to increase **modularity** by breaking down program logic into distinct parts (so-called **concerns**, cohesive areas of functionality).

Quản lý các module theo chiều ngang, quản lý việc gọi các module dọc theo qua trình thực thi process, lúc nào cần gọi và sử dụng part nào của logic.

There are various common good examples of aspects including **logging**, **declarative transactions**, **security**, and **caching** etc.

Whereas DI helps you decouple your application objects from each other, AOP helps you decouple cross-cutting concerns from the objects that they affect.

The AOP module of Spring Framework allowing you to define **method-interceptors** and pointcuts to cleanly decouple code that implements functionality that should be separated.

# Module
Spring could potentially be a one-stop shop for all your enterprise applications, however, Spring is modular, *allowing you to pick and choose which modules are applicable to you*, without have bring in the rest.

The Spring Framework provides *about 20 modules*.

<figure>
  <figcaption style="text-align:center;">Spring Architecture</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img align="middle" src="spring/spring_architecture.png" alt="Spring" title="Spring">
</figure>

## Core Container
Consists of the Core, Beans, Context, and Expression Language modules:
- **Core module**: provides the fundamental parts of the framework, including the **IoC** and **DI** features.
- **Bean module**: provides BeanFactory which is a sophisticated implementation of the **factory pattern**.
- **Context module**: builds on the solid base provided by the Core and Beans modules and it is **a medium to access any objects defined and configured**. The **ApplicationContext interface** is the focal point of the Context module.
- **Expression Language module**: provides a powerful expression language for **querying and manipulating an object graph at runtime**.

## Data Access/Integration
Consists of the JDBC, ORM, OXM, JMS and Transaction modules whose details is as follows:
- **JDBC module**: provides a JDBC-abstraction layer that removes the need to do tedious JDBC related coding.
- **ORM module**: provides *integration layers* for popular **object-relational mapping APIs**, including JPA, JDO, Hibernate, and **iBatis**.
- **OXM module**: provides an *abstraction layer* that supports **Object/XML mapping** implementation for JAXB, Castor, XMLBeans, JiBX and XStream.
- **Java Messaging Service (JMS) module**: contains features for producing and consuming messages.
- **Transaction module**: supports programmatic and declarative transaction management for classes that implement special interfaces and for all your POJOs.
## Web
Consists of the Web, Web-Servlet, Web-Struts, and Web-Portlet modules:
- **Web module**: provides basic web-oriented integration features such as multipart file-upload functionality and the initialization of the IoC container using servlet listeners and a web-riented application context.
- **Web-Servlet module**: contains Spring's MVC imlementation for web applications.
- **Web-Struts module**: contains the support classes for integrating a classic Struts web tier within a Spring application
- **Web-Portlet module**: provides the MVC implementation to be used in a portlet environment and mirrors the functionality of Web-Servlet module.
## Miscellaneous
- **AOP module**: provides aspect-oriented programming implementation allowing you to define method-interceptors and pointcuts to cleanly decouple code that implements functionality that should be separated.
- **Aspects module**: provides integration with AspectJ which is again a powerful and mature aspect oriented programming framework.
- **Instrumentation module**: provides class in instrumentation support and class loader implementation to be used in certain application servers.
- **Test module**: support the testing of Spring components with JUnit or TestNG frameworks.



# Tutorial
## Spring Configuartion Metadata:
There are following three important methods to provide configuration metadata to the Spring Container:
1. XML based configuration file.
2. Annotation-based configuration
3. Java-based configuration.

###  XML based configuration file.
(search string `http://www.springframework.org/schema/beans` in project to show all file config), usually at `WebContent/WEB-INF` directory.

+ **Bean config file**
	* Have many **bean** inject to project, each bean have properties: **id, class, init-method, destroy-method, etc.**
	* Each bean have many **property**: each property have properties: name, value, ref, etc.

			<?xml version="1.0" encoding="UTF-8"?>

			<beans xmlns="http://www.springframework.org/schema/beans"
			    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			    xsi:schemaLocation="http://www.springframework.org/schema/beans
			    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd">

			   <!-- A simple bean definition -->
			   <bean id="..." class="...">
			       <!-- collaborators and configuration for this bean go here -->
			   </bean>

			   <!-- A bean definition with lazy init set on -->
			   <bean id="..." class="..." lazy-init="true">
			       <!-- collaborators and configuration for this bean go here -->
			   </bean>

			   <!-- A bean definition with initialization method -->
			   <bean id="..." class="..." init-method="...">
			       <!-- collaborators and configuration for this bean go here -->
			   </bean>

			   <!-- A bean definition with destruction method -->
			   <bean id="..." class="..." destroy-method="...">
			       <!-- collaborators and configuration for this bean go here -->
			   </bean>

			   <!-- more bean definitions go here -->

			</beans>

+ **Web MVC config file** (web.xml)

			<web-app id="" version="" xmlns="" xmlns:xsi="" xsi:schemaLocation="">
				<servlet>
					<servlet-name>...</servlet-name>
					<servlet-class>...</servlet-class>
					...
				</servlet>

				<servlet-mapping>
					<servlet-name>...</servlet-name>
					<url-pattern>*.jsp</url-pattern>
				</servlet-mapping>

				<!-------- DispatcherServlet definition goes here----->
				....
				<context-param>
				   <param-name>contextConfigLocation</param-name>
				   <param-value>/WEB-INF/HelloWeb-servlet.xml</param-value>
				</context-param>

				<listener>
				   <listener-class>
				      org.springframework.web.context.ContextLoaderListener
				   </listener-class>
				</listener>
			</web-app>

### Annotation-based configuration
Starting from Spring 2.5 it became possible to **configure the dependency injection using annotations**. So instead of using XML to describe a bean wiring, you can move the bean configuration into the component class itself by using annotations on the relevant class, method, or field declaration.

When in application context config file xml have this line : `<context:annotation-config />`
it will specify annotation base configuration. First, Spring will scan context file and create all object of all bean in file and contain in a container.

- `@Autowired`: search in container same **type** of bean and wiring this bean. Use id of bean to search, id of bean is mix camel case of var type.
- `@Qualifier`: use it when want specify what bean will wiring when have same type.
- `@Resource` : search in container same **name** of bean and wiring this bean.


## IoC Containers


## Spring Bean
The objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is **instantiated**, **assembled**, and otherwise **managed by a Spring IoC container**. These beans are created with the configuration metadata that you supply to the container, for example, in the form of XML <bean/> definitions which you have already seen in previous chapters.

The bean definition contains the information called configuration metadata which is needed for the container to know the followings:
- How to create a bean
- Bean's lifecycle details
- Bean's dependencies

All the above configuration metadata translates into a set of the following properties that make up each bean definition:

| Properties               | Description                                                                                                                                          |
| -                        | -                                                                                                                                                    |
| class                    | This attribute is mandatory and specify the bean class to be used to create the bean                                                                 |
| name                     | Specifies the bean identifier uniquely. In XML-based configuration metadata, you use the id and/or name attributes to specify the bean identifier(s) |
| scope                    | Specifies the scope of the objects created from a particular bean definition and it will be discussed in bean scopes chapter.                        |
| constructor-arg          | Used to inject the dependencies and will be discussed in next chapters.                                                                              |
| properties               | Used to inject the dependencies                                                                                                                      |
| autowiring mode          | Used to inject the dependencies                                                                                                                      |
| lazy-initialization mode | A lazy-initialization bean tells the IoC container to create a bean instance when it is first requested, rather than at startup.                     |
| initialization method    | A callback to be called just after all necessary properties on the bean have been set by the container.                                              |
| destruction method       | A callback to be used when the container containing the bean is destroyed.                                                                           |

### Spring Bean Scope
When defining a bean in Spring, you have the option of declaring a scope for that bean. For example, to force Spring to produce a new bean instance each time one is needed, you should declare the bean's scope attribute to be prototype. Similar way if you want Spring to return the same bean instance each time one is needed, you should declare the bean's scope attribute to be singleton.

The Spring Framework supports following five scope, three of which are available only if you use a web-aware ApplicationContext.

| Scope          | Description                                                                                        |
| -              | -                                                                                                  |
| singleton      | Definition to a single instance per Spring IoC container (default) only sindle instance everywhere and everytime                                 |
| prototype      | Definition to have any number of object instances                                                   |
| request        | Definition to an HTTP request. Only valid in the context of a web-aware Spring ApplicationContext. |
| session        | Definition to an HTTP session. Only valid in the context of a web-aware Spring ApplicationContext. |
| global-session | Definition to a global HTTP session. Only valid in the context of a web-aware Spring ApplicationContext. |

#### The singleton scope
If scope is set to singleton, the Spring IoC container creates exactly one instance of the object defined by that bean definition. This single instance is stored in a cache of such singleton beans, and all subsequent requests and references for that named bean return the cached object.

The default scope is always singleton however, when you need one and only one instance of a bean, you can set the scope property to singleton in the bean configuration file, as shown below:

	<!-- A bean definition with singleton scope -->
	<bean id="..." class="..." scope="singleton">
	    <!-- collaborators and configuration for this bean go here -->
	</bean>

#### The prototype scope
If scope is set to prototype, the Spring IoC container creates new bean instance of the object every time a request for that specific bean is made. As a rule, use the prototype scope for all state-full beans and the singleton scope for stateless beans.

To define a prototype scope, you can set the scope property to prototype in the bean configuration file, as shown below:

	<!-- A bean definition with singleton scope -->
	<bean id="..." class="..." scope="prototype">
	    <!-- collaborators and configuration for this bean go here -->
	</bean>

### Spring Bean Life Cycle
The life cycle of a Spring bean is easy to understand. When a bean is **instantiated**, it may be required to perform some initialization to get it into a usable state. Similarly, when the bean is no longer required and is removed from the container, some cleanup may be required.

Though, there is lists of the activities that take place behind the scenes between the time of bean Instantiation and its **destruction**


## Spring Dependency Injection
When writing a complex Java application, application classes should be as independent as possible of other Java classes to increase the possibility to reuse these classes and to test them independently of other classes while doing unit testing. **Dependency Injection** (or sometime called **wiring**) helps in gluing these classes together and same time keeping them independent.

You can mix both, **Constructor-based** and **Setter-based** DI but it is a good rule of thumb to use *constructor arguments for mandatory dependencies* and *setters for optional dependencies*.

### [Constructor-based dependency injection](http://www.tutorialspoint.com/spring/constructor_based_dependency_injection.htm)


### [Spring Setter-based Dependency Injection](http://www.tutorialspoint.com/spring/setter_based_dependency_injection.htm)
