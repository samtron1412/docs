[TOC]

# Overview
In Engineer view, we need experience and compare between products to choose right product at each specific conditions.

# Web development
## [Active Record vs Data Mapper](http://culttt.com/2014/06/18/whats-difference-active-record-data-mapper/)

## [Doctrine 2 vs Eloquent](http://culttt.com/2014/07/07/doctrine-2-different-eloquent/)

## [nginx vs apache](https://www.digitalocean.com/community/tutorials/apache-vs-nginx-practical-considerations#distributed-vs-centralized-configuration)
### General
- **Apache** is often chosen by administrators for its flexibility, power, and widespread support. It is extensible through a dynamically loadable module system and can process a large number of interpreted languages without connecting out to separate software.
- **Nginx** is often selected by administrators for its resource efficiency and responsiveness under load.

### Connection Handling Architecture
- **Apache** provides a variety of multi-processing modules (Apache calls these MPMs) that dictate how client requests are handled.
	+ **mpm_prefork** : process
	+ **mpm_worker** : threaded
	+ **mpm_event** : event handle like Nginx, stable with Apache 2.4
- **Nginx** was designed from the ground up to use an *asynchronous*, *non-blocking*, *event-driven* connection handling algorithm.

### Static vs Dynamic content
- Rather than using the *embedded interpreter* approach, Nginx hands off dynamic content to *CGI, FastCGI, or even other web severs like Apache*, which is then passed back to Nginx for delivery to the client.
- **Nginx** does not have any ability to process dynamic content natively. To handle PHP and other requests for dynamic content, Nginx must pass to an external processor for execution and wait for the rendered content to be sent back. The results can then be relayed to the client. **Apache** can also process dynamic content by embedding a processor of the language in question into each of its worker instances.

### Distributed vs Centralized Configuration


### File vs URI-Based Interpretation


### Modules


### Support, Compatibility, Ecosystem, and Documentation


### Using Apache and Nginx Together

# Editor - IDE
## vim vs Emacs
- http://unix.stackexchange.com/questions/986/what-are-the-pros-and-cons-of-vim-and-emacs
-


# Toyota vs Honda vs Hyundai
Toyota is the most popular.

Honda is the next.
