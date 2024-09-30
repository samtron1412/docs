# Overview

- Manifesto for Agile Software Development
    + https://agilemanifesto.org/
    + Twelve Principles of Agile Software
        * https://agilemanifesto.org/principles.html
- Implementation of the above Manifesto and Principles
    + Scrum framework
    + Kanban framework

# Manifesto

We are uncovering better ways of developing
software by doing it and helping others do it.
Through this work we have come to value:

- **Individuals and interactions** over processes and tools
- **Working software** over comprehensive documentation
- **Customer collaboration** over contract negotiation
- **Responding to change** over following a plan

That is, while there is value in the items on
the right, we value the items on the left more.

# Principles

We follow these principles:

1. Our highest priority is to satisfy the customer through early and
   continuous delivery of valuable software.
2. Welcome changing requirements, even late in development. Agile
   processes harness change for the customer's competitive advantage.
3. Deliver working software frequently, from a couple of weeks to a
   couple of months, with a preference to the shorter timescale.
4. Business people and developers must work together daily throughout
   the project.
5. Build projects around motivated individuals.  Give them the
   environment and support they need, and trust them to get the job
   done.
6. The most efficient and effective method of conveying information to
   and within a development team is face-to-face conversation.
7. Working software is the primary measure of progress.
8. Agile processes promote sustainable development.  The sponsors,
   developers, and users should be able to maintain a constant pace
   indefinitely.
9. Continuous attention to technical excellence and good design enhances
   agility.
10. Simplicity--the art of maximizing the amount of work not done--is
    essential.
11. The best architectures, requirements, and designs emerge from
    self-organizing teams.
12. At regular intervals, the team reflects on how to become more
    effective, then tunes and adjusts its behavior accordingly.

# Some common concepts

- `Workflow`
    + A series of states: tasks transition from one state to another
    + TO DO / INPUT QUEUE: work that has not been started
    + IN PROGRESS / IMPLEMENTATION: work that is actively being looked
      at by the team
    + CODE REVIEW: work that is completed and awaiting review
    + RELEASE: work passed the review but haven't deployed to Prod yet
    + DONE: work is deployed to Prod or whatever team's definition of
      done
- `Stories`: "user stories", are short requirements or requests written
  from the perspective of an end user.
    + Usually can be completed in one or two-week sprint.
- `Epics` are large bodies of work that can be broken down into a number
  of smaller tasks (called stories).
- `Initiatives`: are collections of epics that drive toward a common
  goal.
- `Estimation`
    + Playing poker: https://www.atlassian.com/blog/platform/scrum-poker-for-agile-projects
        * Lending an equal voice to everyone in the team
        * Identifying gaps in requirement and implementation
        * Better estimation


# Scrum

- Enhance Scrum using: User Story, Planning Poker, Test Driven
  Development, Refactoring, Continuous Integration, and Pair Programming
    + Kanban board: is used to visualize tasks (to do, doing, done)
    + Burn-down chart: is used to visualize how much work is yet to be
      done to reach the sprint goal.

## Sprints

- A sprint is a short, time-boxed period when a scrum team works to
  complete a set amount of work.
    +  Usually one to two weeks.

## Ceremonies (meetings / events)

### Sprint Planning

- Attendees: development team, scrum master, product owner
- When: at the beginning of a Sprint
- Duration: usually around 1 hour per week of iteration, so a two-week
  Sprint needs 2 hour meeting.
- Agile framework: Scrum (Kanban does have planning meeting, but not on
  a fixed iteration schedule with formal Sprint planning)
- Purpose
    + Use the sprint planning meeting to flesh out intimate details of
      the work that needs to get done.
    + Encourage team members to sketch out tasks for all stories, bugs,
      and tasks that come into the sprint.

### Daily Stand-up

- Attendees: development team, scrum master, product owner
- When: once per day, typically in the morning
- Duration: no more than 15 minutes.
    + Don't book a conference room and conduct the stand-up sitting
      down. Standing up helps keep the meeting short!
- Agile framework: Scrum and Kanban
- Purpose: quickly inform everyone of what's going on across the team
    + Have each team member answers the following questions:
        * What did I complete yesterday?
        * What will I work on today?
        * Am I blocked by anything?

### Sprint review / demo

- Attendees: dev team, scrum master, product owner
- When: at the end of a Sprint
- Duration: typically 45 minutes per week of iteration
- Agile framework: Scrum and Kanban
    + Scrum teams do Sprint retrospectives based on a fixed cadence.
    + Kanban teams can benefit from occasional retrospectives, too.
- Purpose: to showcase the work of the team.
    + celebrate their accomplishments, demonstrate work finished within
      the iteration.

### Sprint retrospective

- A sprint retrospective is a meeting to review what was successful
  during the sprint and what can be improved upon.
- Attendees: dev team, scrum master, product owner
- When: at the end of a Sprint
- Duration: typically 45 minutes per week of iteration
- Agile framework: Scrum and Kanban
    + Scrum teams do Sprint retrospectives based on a fixed cadence.
    + Kanban teams can benefit from occasional retrospectives, too.
- Purpose: to showcase the work of the team.
    + celebrate their accomplishments, demonstrate work finished within
      the iteration.

## KPI (key performance indicator) metrics to optimize delivery

### Sprint burndown

- A sprint burndown report then tracks the completion of work throughout
  the sprint. The x-axis represents time, and the y-axis refers to the
  amount of work left to complete, measured in either story points or
  hours.
- Anti patterns to watch for
    + The team finishes early sprint after sprint because they aren't
      committing to enough work.
    + The team misses their forecast sprint after sprint because they're
      committing to too much work.
    + The burndown line makes steep drops rather than a more gradual
      burndown because the work hasn't been broken down into granular
      pieces.
    + The product owner adds or changes the scope mid-sprint.

### Velocity

- Velocity is the average amount of work a scrum team completes during a
  sprint, measured in either story points or hours, and is very useful
  for forecasting.
- Anti patterns
    + When velocity is erratic over a long period of time, always revisit the team's estimation practices. During the team's retrospective, ask the following questions:
        * Are there unforeseen development challenges we didn't account for when estimating this work? How can we better break down work to uncover some of these challenges?
        * Is there outside business pressure pushing the team beyond its limits? Is adherance to development best practices suffering as a result?
        * As a team, are we overzealous in forecasting for the sprint?

### Cumulative flow diagram

- The cumulative flow diagram should look smooth(ish) from left to
  right. Bubbles or gaps in any one color indicate shortages and
  bottlenecks, so when you see one, look for ways to smooth out color
  bands across the chart.
- Anti patterns
    + Blocking issues create large backups in some parts of the process and starvation in others.
    + Unchecked backlog growth over time. This results from product owners not closing issues that are obsolete or simply too low in priority to ever be pulled in.

### Control chart

- Control charts focus on the cycle time of individual issues–the total
  time from "in progress" to "done". Teams with shorter cycle times are
  likely to have higher throughput, and teams with consistent cycle
  times across many issues are more predictable in delivering work.
- Anti patterns
    + Control charts can appear fickle at first. Don't be so concerned with every outlier. Look for trends. Here are two areas to watch out for:
        * Increasing cycle time - Increasing cycle time saps the team of
          its hard-earned agility. In the team retrospective, take time
          to understand an increase. One exception: if the team's
          definition of done has expanded, cycle time will probably
          expand too.
        * Erratic cycle time – The goal is to have consistent cycle time
          for work items that have similar story point values. Filter
          the control chart for each story point value to check for
          consistency. If cycle time is erratic on small and large story
          point values, spend time in the retrospective examining the
          misses and improving future estimation.

### Epic and release burndown

- Epic and release (or version) burndown charts track the progress of
  development over a larger body of work than the sprint burndown, and
  guide development for both scrum and kanban teams.
- Anti patterns to watch for
    + Epic or release forecasts aren't updated as the team churns through the work.
    + No progress is made over a period of several iterations.
    + Chronic scope creep, which may be a sign that the product owner doesn't fully understand the problem that body of work is trying to solve.
    + Scope grows faster than the team can absorbzi it.
    + The team isn't shipping incremental releases throughout the development of an epic.


# Kanban

- No fixed schedule such as Scrum.
- Having WIP limit.

## Lead time vs Cycle time

When discussing the importance of workflow in Kanban, two primary
notions come into play lead time and cycle time. What is the difference
between them, and how can we measure them?

> Lead time is mainly a period. It starts when a request enters the work
> cycle and is in the "ready to start" phase and ends when the request is
> "completed."

The following example better illustrates the concept behind lead time:

Let's say you placed a dinner order at 8:00 p.m. and your order gets
delivered at 8:30 p.m. your lead time, in this case, is 30 minutes.

It's the period from the moment you placed a request until you got your
request delivered.

> Cycle time is how much time a resource spends on a task. For example,
> cycle time starts when a team member processes a request from the
> "in-progress" status until the "completion" status.

Back to the dinner example, cycle time is when the chef starts preparing
your order. Let's say the kitchen received it at 8:10 p.m. You get your
food delivered at 8:30 p.m; in this case, your cycle time is 20
minutes. It is the actual time needed to process your order.

### How are both times measured?

The main difference between lead time and cycle time is their unit of
measurement. Lead time is measured by seconds, hours, and weeks, whereas
cycle time is measured by the time spent per task, unit, or process.

### What is their relationship, and how can we calculate it?

`Lead time = Cycle time x Work in Progress (WIP)`

The purpose of this formula is to render the entire process predictable,
allowing you to reliably forecast project completion with minimal loss
and enabling you to outpace your competitors with faster, more efficient
output.

### Calculating lead-time vs. cycle time to ensure a better flow

The truth behind the flow of work is not how fast an item moves through
the cycle but how smoothly it flows from start to end. And that's what
matters. Limiting work in progress is of utmost importance as to why the
Kanban method works well. It may sound unrealistic, but limiting work in
progress refers to how many tasks can be started at once.

# Gantt chart / Roadmap / Timeline

- A Gantt chart is a project management tool that illustrates work
  completed over a period of time in relation to the time planned for
  the work.
- A Gantt chart can include the start and end dates of tasks,
  milestones, dependencies between tasks, assignees, and more.
