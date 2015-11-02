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

# Certification vs Diploma vs Degree
## Certification
Certification programs are specialized and industry specific. These programs don't offer a broad overview of a field or industry, and are often a good option for someone who already has a degree or work experience in the field.

## Diploma
Diploma programs are specialized but more in depth than certification programs. Diplomas are also what you receive upon graduating high school.

## Degree
Degree programs are awarded by colleges and universities. A degree program is often requires the student o take general education courses to support a more rounded education.
	+ An **associate's degree** is two-year degree most commonly granted by a community college or technical school. They can also be granted by four-year colleges and universities.
	+ A **bachelor's degree** is a four-year degree that is granted by a college or university.
	+ A **master's degree** is what is called a post-graduate degree because you go on to get one only after you have graduated with your bachelor's.
	+ A **Ph.D** is another example or a post-graduate degree, and is several more years of study and intensive research.

# Thesis vs Dissertation
The differences between a thesis and a dissertation it really depends upon the requirements set forth by each specific school or academic program. Most universities make their dissertation/thesis guidelines available online so it's best to view them ahead of time so you aware of what will be required of you.

In USA
1. A thesis is submitted **at the end of one's master's degree**, and a dissertation is submitted **at the end of a PhD**.
2. For a thesis, you have **conduct original research**, while for a dissertation you have to **synthesize already existing literature**.
3. Thesis analysis **is added to the already existing literature**, while dissertation is **an analysis of the existing literature**.
