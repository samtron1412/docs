[TOC]

# Overview

`Representational state transfer` (REST) is a software architectural style
that was created to guide the design and development of the architecture
for the World Wide Web.
- REST defines a set of constraints (6) for how the architecture of an
  Internet-scale distributed hypermedia system, such as the Web, should
  behave.
- A web API that obeys the REST constraints is informally described as
  `REASTful`.
- The goal of REST is to increase performance, scalability, simplicity,
  modifiability, visibility, portability, and reliability.

# What does Representational State Transfer (REST) mean? Etymology

The term representational state transfer was introduced and defined in
2000 by Roy Fielding in his doctoral dissertation.
- The term is intended to evoke an image of how a well-designed Web
  application behaves:
- it is a network of Web resources (a virtual state machine) where the
  user advances through the application by selecting links resulting in
  the next resource's representation (the next application state) being
  transferred to the client and rendered for the user.

# REST Constraints (6)

- Client-server architecture
- Statelessness
    + no session information is retained by the server
    + relevant session data is sent to the server by the client in such
      a way that every packet of information transferred can be
      understood in isolation without context information from previous
      packets in the session.
- Cacheability
- Layered system
- Code on demand (optional)
- Uniform interface
    + This is the most fundamental constraint of any RESTful system.
    + It simplifies and decouples the architecture, which enables each
      part to evolve independently.
    + There are 4 sub-constraints
        * Resource identification in requests
        * Resource manipulation through representations - when a client
          holds a representation of a resource, including any metadata
          attached, it has enough information to modify or delete the
          resource's state.
        * Self-descriptive messages - each message includes enough
          information to describe how to process the message.
        * Hypermedia as the engine of application state (HATEOAS) -
          having an initial URI for the REST application, a REST client
          should then be able to use server-provided links dynamically
          to discover all the available resources it needs.
            - As access proceeds, the server responds with text that
              includes hyperlinks to other resources that are currently
              available.
            - There is no need for the client to be hard-coded with
              information regarding the structure or dynamics of the
              application.

# Tutorials and Learn more

- https://www.restapitutorial.com/
- https://medium.com/@andrea.chiarelli/please-dont-call-them-restful-d2465527b5c
- https://restfulapi.net/

# References

[wiki]: https://en.wikipedia.org/wiki/Representational_state_transfer
