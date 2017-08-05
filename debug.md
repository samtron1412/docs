[TOC]

# Overview

Debugging is the process of finding and resolving of defects that
prevent correct operation of computer software or a system.
- Debugging tactics can involve interactive debugging, control flow
  analysis, unit testing, integration testing, log file analysis,
  monitoring at the application or system level, memory dumps, and
  profiling.

## History

The terms "bug" and "debugging" are popularly attributed to Admiral
Grace Hopper in the 1940s. While she was working on a Mark II computer
at Harvard University, her associated discovered a moth stuck in a relay
and thereby impeding operation, whereupon she remarked that they were
"debugging" the system.

However, the term "bug" in the meaning of technical error dates back at
least to 1878 and Thomas Edison. Similarly, the term "debugging" seems
to have been used as a term in aeronautics before entering the world of
computers.

# Tools

## Debugger


# Debugging Process

## Bug report

>A good bug report is one that describes the problem well enough that
>someone familiar with the project can understand and act on that bug
>report without talking to the person who wrote it.

A good bug report has all of the following:

1. **a descriptive title**, one that contains specific key words and
   terms to enable categorization.

not good: “An application named Finder should not lose my files” good:
“Icons can be placed offscreen, and lost”

2. **a summary of the situation**, which describes the problem at a high
   level, in a way that anyone familiar with the project can understand.

not good: “Can’t save images.” good: “Every time I try to save a large
image to the photo library, the app crashes.”

3. **a set of steps to recreate the situation**.  These should start
   with launching the app, include any relevant configuration steps, be
   atomic, be specific, end with the action that causes the problem to
   be visible.

While these steps may sometimes seem unnecessary, they are very valuable
when you want to close the bug. You cannot verify the fix without a
specific set of steps. How would you know that this was the workflow
that the tester used?

4. **the expected behavior**, and why the observed behavior is
   different.

This leads to more Aha! moments than you would imagine. Many of the
details left out of the description will appear here.

5. **the severity of the issue**.  When this happens, how bad is it?

It’s important to be clear on your reasoning as to why this is the worst
bug you’ve seen in your lifetime, so that others can understand and
support your decision.

6. **the frequency of the issue**.  How often does this occur? Always?
   Once?

The general nature of a problem is often not enough to characterize that
problem. One also needs to know the frequency. Is a crash always a
Critical bug?  No.  Not if it was only seen once in 6 months of
development. Is a pixel alignment issue always Minor?  No.  Not when it
appears at an obvious point in every launch. Frequency can make a big
difference to the overall severity of a problem.

7. **a description of the context** in which the problem was found - the
   specific system, device, or OS, and any relevant configuration
   options for the test environment.
    - build # of the product under development
    - type of hardware on which test was run, e.g. iPhone, iPad, Mac
    - configuration of hardware, e.g. 8Gb iPhone 3G, 32Gb iPad 3G
    - OS version / build # on that hardware
    - any special conditions, e.g. on wifi, after low battery warning

----

have **images** that show UI problems and **sample code** that
demonstrates API problems.

If you’re writing a bug about a user interface issue, take a screenshot
or two. Feel free add circles and arrows that make it clear where the
problem is. When you can, show the correct UI and then the problem.
That helps everyone more quickly understand the issue.

Likewise, if you’re writing a bug which involves an API, attach a sample
project which exhibits the problem. This helps to ensure that the
problem is not related to something in your project, and also makes it
much easier for your API vendor to investigate.

# Techniques

# Anti-debugging

# References
