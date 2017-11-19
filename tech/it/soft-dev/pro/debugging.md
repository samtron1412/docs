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

Generally, high-level programming languages, such as Java make debugging
easier, because they have features such as exception handling that make
real sources of erratic behavior easier to spot.
- In programming languages such as C or assembly, bugs may cause silent
  problems such as memory corruption, and it is often difficult to see
  where the initial problem happened.
- In those cases, memory debugger tools may be needed.

Static code analysis tools
- These tools look for a very specific set of known problems, some
  common and some rare, within the source code.
- All such issues detected by these tools would rarely be picked up by a
  compiler or interpreter, thus they are not syntax checkers, but more
  semantic checkers.

## Debugger

Debuggers are software tools which enable the programmer to monitor the
execution of a program, stop it, restart it, set breakpoints, and change
values in memory.
- The term "debugger" can also refer to the person who is doing the
  debugging.


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

# Common bugs

## Off-by-one error

An off-by-one error is a logic error involving the discrete equivalent
of a boundary condition.
+ It often occurs in an iterative loop when it iterates one time too
  many or too few.
+ This problem could arise when a programmer makes mistakes such as
  using "is less than or equal to" where " is less than" should have
  been used in a comparison, or fails to take into account that a
  sequence starts at zero rather than one.

### C standard library `strncat`

The `strncat` function will write a terminating null character one bute
beyond the maximum length specified. The following code contains such a
bug:

```c
void foo (char* s)
{
    char buf[15];
    memset(buf, 0, sizeof(buf));
    strncat(buf, s, sizeof(buf)); // Final parameter should be: sizeof
    // (buf) - 1.
}
```

Off-by-one errors are common in using the C library because it is not
consistent with respect to whether one needs to subtract 1
byte-functions. When `fgets()` and `strncpy` will never write past the
length given them, `strncat` will write past the length given them.
- On some systems (little endian architectures in particular) this can
  result in the overwriting of the least significant byte of the frame
  pointer. This can cause an exploitable condition where an attacker can
  hijack the local variables for the calling routine.
- One approach that often helps avoid such problems is to use variants
  of these functions that calculate how much to write based on the total
  length of the buffer, rather than the maximum number of characters to
  write. Such functions include `strlcat` adn `strlcpy`

# References

1. [How to fix bugs, step by step][1]
2. [MIT Invented a way to automatically fix software bugs][2]
3. [MIT News automatic bug repair][3]
4. [Two techniques for automatically eliminating software defects][4]

[1]: http://www.yacoset.com/Home/how-to-fix-bugs-step-by-step "How to fix bugs, step by step"
[2]: http://gizmodo.com/mit-invented-a-way-to-fix-software-bugs-autonomously-wi-1714669000 "MIT invented a way to automatically fix software bugs"
[3]: http://news.mit.edu/2015/automatic-code-bug-repair-0629 "MIT News automatic bug repair"
[4]: http://www.srl.inf.ethz.ch/workshop2014/eth-rinard.pdf "Two techniques for automatically eliminating software defects"
