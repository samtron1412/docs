[TOC]

# Overview

## Resources

- No silver bullets for Software Development
    + https://web.archive.org/web/20160910002130/http://worrydream.com/refs/Brooks-NoSilverBullet.pdf
- Google Software Engineering
    + https://abseil.io/resources/swe-book/html/toc.html

### Books

- [Amazon][amazon]
- [Goodreads][read]

# Project Management

- https://www.cio.com/article/287088/project-management-how-to-design-a-successful-raci-project-plan.html
- https://www.teamgantt.com/blog/raci-chart-definition-tips-and-example
- The RACI matrix
    + lists out every task, milestone, or key decision involved in
      completing a project and
    + assigns which roles are `Responsible` for each action item, which
      personnel are `Accountable`, and, where appropriate, who needs to
      be `Consulted` or `Informed`.
- `Responsible`: People or stakeholders who do the work. They must
  complete the task or objective or make the decision. Several people
  can be jointly Responsible.
- `Accountable`: Person or stakeholder who is the “owner” of the
  work. He or she must sign off or approve when the task, objective or
  decision is complete. This person must make sure that responsibilities
  are assigned in the matrix for all related activities. Success
  requires that there is only one person Accountable, which means that
  “the buck stops there.”
- `Consulted`: People or stakeholders who need to give input before the
  work can be done and signed-off on. These people are “in the loop” and
  active participants.
- `Informed`: People or stakeholders who need to be kept “in the
  picture.” They need updates on progress or decisions, but they do not
  need to be formally consulted, nor do they contribute directly to the
  task or decision.

# Software development life cycle/process/methodology/model

- In recent years, industry adopted a holistic view of a software
  development team where development teams communicate more with
  stakeholders / users including operation teams.
- A modern software engineer is an IT generalist who should have a
  wide-ranging knowledge of both development and operations, including
  coding, infrastructure management, system administration, and DevOps
  toolchains.
    + DevOps engineers should also possess interpersonal skills since
      they work across company silos to create a more collaborative
      environment.

## Agile

- Agile software development
    + https://en.wikipedia.org/wiki/Agile_software_development
- Agile software development values
    + Individuals and interactions over processes and tools
    + Working software over comprehensive documentation
    + Customer collaboration over contract negotiation
    + Responding to change over following a plan
- Agile software development principles: 12
    + Customer satisfaction by early and continuous delivery of valuable software.
    + Welcome changing requirements, even in late development.
    + Deliver working software frequently (weeks rather than months)
    + Close, daily cooperation between business people and developers
    + Projects are built around motivated individuals, who should be trusted
    + Face-to-face conversation is the best form of communication (co-location)
    + Working software is the primary measure of progress
    + Sustainable development, able to maintain a constant pace
    + Continuous attention to technical excellence and good design
    + Simplicity—the art of maximizing the amount of work not done—is essential
    + Best architectures, requirements, and designs emerge from self-organizing teams
    + Regularly, the team reflects on how to become more effective, and adjusts accordingly

## DevOps

- Google Cloud: The Accelerate State of DevOps Report
    + https://dora.dev/
    + https://dora.dev/devops-capabilities/technical/continuous-delivery/
    + https://services.google.com/fh/files/misc/2023_final_report_sodr.pdf
    + https://services.google.com/fh/files/misc/2022_state_of_devops_report.pdf
- https://www.atlassian.com/devops
- DevOps is a set of practices that works to automate and integrate the
  processes between software development and system operation teams, so
  they can build, test, and release software faster and more reliably.
    + Integrate the development and operation teams
- History
    + The DevOps movement started to coalesce some time between 2007 and
      2008
- Going beyond Agile
    + Agile methodologies help teams plan and produce by breaking work
      down into manageable tasks and milestones.
        * https://www.atlassian.com/agile
    + Continuous integration and delivery: automating the merging and
      deployment of code.
        * https://www.atlassian.com/continuous-delivery
    + Git repositories and workflows
        * https://www.atlassian.com/git
    + Incident management: responding to issues and trouble tickets
        * https://www.atlassian.com/incident-management
- Benefits of DevOps
    + Collaborating and trust
    + Release faster and work smarter
    + Accelerate time-to-resolution
    + Better manage unplanned work: better Mean Time to Recovery (MTTR)
      when incidents and outages occur
- DevOps culture
    + Transparency, communication, and collaboration
    + Shared responsibilities
    + Fast feedback
    + Automation

# Core Activities

## Identification of need

## Planning

- Business + Technical -> Requirements

## Design and Documenting

- Design documents
    + Architecture, Infrastructure, Data structures, Logic

## Implementation

- Pseudo-code for each component in the design document
- Keep the code reviews to be small and testable pieces of code
    + Easier to be reviewed and get approvals
- Effectiveness
    + Focus on the goal and be realistic
    + Try to clear roadblocks to ship code
    + APM (actions per minutes): submit as least one CR per day
    + Asking for help when you need it, to save time: asking experienced
      engineer
- Be nice with the tech lead
    + Send out diff to the tech lead email, and ask him to patch it
    + Put teach lead name on the design document

## Testing

- Listing out all the things that we explicitly or implicitly test in
  manual testing:
    + Serialization/deserialization
    + Functional
    + etc.
- Try to automate all of that manual testing as much as possible
    + Unit tests: serialization/deserialization
    + Integration tests: end-to-end testing

## Debugging

## Deployment

- [Continuous Integration, Continuous Deployment and Continuous Delivery](http://stackoverflow.com/questions/28608015/continuous-integration-vs-continuous-delivery-vs-continuous-deployment)

### [Continuous Integration](http://martinfowler.com/articles/continuousIntegration.html)

#### Hosted Services

- [Circle CI](https://circleci.com/)
- [Travis CI](https://travis-ci.org/)
- [Wercker](http://wercker.com/): using it because unlimited private repositories.
- [Jenkins](https://jenkins.io/)

### Continuous Deployment

- [Codeship](https://codeship.com/)

### Continuous Delivery

http://continuousdelivery.com/

![Continuous Delivery Story Line](../graphic/software/continuous-delivery-storyline.png)

## Maintenance

# Enterprise Application Development

- Other books
    + https://itnext.io/recommended-reading-list-for-enterprise-software-developers-and-architects-b77c905b2dbd

## Architecture And Design Patterns

- Books:
    + "Patterns of Enterprise Application Architecture" by Martin Fowler: Offers a tutorial and over 40 patterns for common enterprise problems, with code examples in Java or C#.
    + "Design Patterns: Elements of Reusable Object-Oriented Software" (The Gang of Four): A foundational text that introduces essential design patterns.
    + "Domain-Driven Design: Tackling Complexity in the Heart of Software" by Eric Evans: A crucial book for building complex software systems by focusing on the core business domain.
- https://en.wikipedia.org/wiki/Architectural_pattern
- Read `design-pattern.md`

## Software Craftsmanship and Principles

- Books:
    + "Refactoring: Improving the Design of Existing Code" by Martin Fowler: Provides patterns and examples for making code more maintainable.
    + "Clean Code: A Handbook of Agile Software Craftsmanship" by Robert C. Martin: Focuses on writing clean, readable, and maintainable code.
    + "The Pragmatic Programmer" by Andrew Hunt and David Thomas: Offers practical advice and wisdom for software developers at all levels.

## Large-scale Systems and Integration

- Books
    + "Designing Data-Intensive Applications" by Martin Kleppmann: Provides a comprehensive overview of distributed systems needed to build large-scale applications.
    + "Enterprise Integration Patterns" by Gregor Hohpe and Bobby Woolf: Covers messaging solutions for integrating enterprise applications.

## Methodologies and Management

- Books
    + "Code Complete" by Steve McConnell: A classic tome on software construction, quality assurance, and craftsmanship.
    + "The Phoenix Project" by Gene Kim, Kevin Behr, and George Spafford: A novel that uses storytelling to explain DevOps principles in a realistic setting.
    + "Accelerate: The Science of Lean Software and DevOps" by Nicole Forsgren, Jez Humble, and Gene Kim: Explains the principles behind high-performing technology organizations.

# Tools
- [Open Source Scrum project management](https://github.com/taigaio)
- [Example of company guide](https://github.com/thoughtbot/guides)

# Career

- https://blog.tryexponent.com/learn-software-engineering-levels-to-advance-your-career/
- https://medium.com/better-programming/the-road-from-junior-to-senior-developer-20b4c850d7dd
- https://codingsans.com/blog/from-junior-to-senior-developer
- Levels
    + Junior Software Engineer
    + Senior Software Engineer
    + Staff Engineer (Senior Staff Engineer)
    + Principal Engineer
    + Distinguished Engineer / Fellow

# References

[wiki]: https://en.wikipedia.org/wiki/Software_development
[processes]: https://en.wikipedia.org/wiki/Software_development_process
[amazon]: https://www.amazon.com/Software-Development-Design-Programming-Books/b?ie=UTF8&node=4016
[read]: https://www.goodreads.com/shelf/show/software-development
