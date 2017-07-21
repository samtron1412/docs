[TOC]

# Overview

- Computer programming is a process that leads from an original
  formulation of a computing problem to executable computer programs.
- Programming involves activities such as analysis and developing
  algorithms

## History

- The first computer program is generally dated to 1843, when
  mathematician Ada Lovelace published an algorithm to calculate a
  sequence of Bernoulli numbers, intended to be carried out by Charles
  Babbage's Analytical Engine.
- In the 1880s Herman Hollerith invented the concept of storing data in
  machine-readable form.
- In 1949, with the concept of the stored-program computers introduced,
  both programs and data were stored and manipulated in the same way in
  the computer memory: Von Newmann and Harvard architecture.
- Machine code was the language of early programs, written in the
  instruction set of the particular machine, often in binary notation.
- Assembly languages were soon developed that let the programmer specify
  instruction in a text format, with abbreviations for each operation
  code and meaningful names of specifying addresses.
    + However, because an assembly language is little more than a
      different notation for a machine language, any two machines with
      different instruction sets also have different assembly languages.
- High-level languages allow the programmer to write programs in terms
  that are more abstract, and less bound to the underlying hardware.

# Principles of Good Programming

The principles of good programming are closely related to principles of
good design and engineering. The following programming principles have
helped me over the years become a better programmer, and I believe can
help any developer become more efficient and to produce code which is
easier to maintain and that has fewer defects.

**DRY** - Don’t repeat yourself - This is probably the single most
fundamental tenet in programming is to avoid repetition. Many
programming constructs exist solely for that purpose (e.g. loops,
functions, classes, and more). As soon as you start repeating yourself
(e.g. a long expression, a series of statements, same concept) create a
new abstraction.
[DRY](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

**Abstraction Principle** - Related to DRY is the abstraction principle
“Each significant piece of functionality in a program should be
implemented in just one place in the source code.”
[ABS](http://en.wikipedia.org/wiki/Abstraction_principle_(programming))

**KISS** (Keep it simple, stupid!) - Simplicity (and avoiding
complexity) should always be a key goal. Simple code takes less time to
write, has fewer bugs, and is easier to modify.
[KISS](http://en.wikipedia.org/wiki/KISS_principle)

**Avoid Creating a YAGNI** (You aren’t going to need it) - You should
try not to add functionality until you need it.
[YABNI](http://en.wikipedia.org/wiki/YAGNI)

**Do the simplest thing that could possibly work** - A good question to
ask one’s self when programming is “What is the simplest thing that
could possibly work?” This helps keep us on the path towards simplicity
in the design.
[simple](http://c2.com/xp/DoTheSimplestThingThatCouldPossiblyWork.html)

**Don’t make me think** - This is actually the title of a book by Steve
Krug on web usability that is also relevant in programming. The point is
that code should be easily read and understood with a minimum of effort
required. If code requires too much thinking from an observer to
understand, then it can probably stand to be simplified
[TOC](http://www.sensible.com/dmmt.html)

**Open/Closed Principle** - Software entities (classes, modules,
functions, etc.) should be open for extension, but closed for
modification. In other words, don't write classes that people can
modify, write classes that people can extend.
http://en.wikipedia.org/wiki/Open_Closed_Principle

**Write Code for the Maintainer** - Almost any code that is worth
writing is worth maintaining in the future, either by you or by someone
else. The future you who has to maintain code often remembers as much of
the code, as a complete stranger, so you might as well always write for
someone else. A memorable way to remember this is “Always code as if the
person who ends up maintaining your code is a violent psychopath who
knows where you live.”
[TOC](http://c2.com/cgi/wiki?CodeForTheMaintainer)

**Principle of least astonishment** - The principle of least
astonishment is usually referenced in regards to the user interface, but
the same principle applies to written code. Code should surprise the
reader as little as possible. The means following standard conventions,
code should do what the comments and name suggest, and potentially
surprising side effects should be avoided as much as possible.
[TOC](http://en.wikipedia.org/wiki/Principle_of_least_astonishment)

**Single Responsibility Principle** - A component of code (e.g. class or
function) should perform a single well defined task.
[TOC](http://en.wikipedia.org/wiki/Single_responsibility_principle)

**Minimize Coupling** - Any section of code (code block, function,
class, etc) should minimize the dependencies on other areas of code.
This is achieved by using shared variables as little as possible. “Low
coupling is often a sign of a well-structured computer system and a good
design, and when combined with high cohesion, supports the general goals
of high readability and maintainability”
[TOC](http://en.wikipedia.org/wiki/Coupling_(computer_programming))

**Maximize Cohesion** - Code that has similar functionality should be
found within the same component.
[TOC](http://en.wikipedia.org/wiki/Cohesion_(computer_science))

**Hide Implementation Details** - Hiding implementation details allows
change to the implementation of a code component while minimally
affecting any other modules that use that component.
[hide](http://en.wikipedia.org/wiki/Information_Hiding)

**Law of Demeter** - Code components should only communicate with their
direct relations (e.g. classes that they inherit from, objects that they
contain, objects passed by argument, etc.)
[Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter)

**Avoid Premature Optimization** - Don’t even think about optimization
unless your code is working, but slower than you want. Only then should
you start thinking about optimizing, and then only with the aid of
empirical data. "We should forget about small efficiencies, say about
97% of the time: premature optimization is the root of all evil" -
Donald Knuth.
[Optimization](http://en.wikipedia.org/wiki/Program_optimization)

**Code Reuse is Good** - Not very pithy, but as good a principle as any
other. Reusing code improves code reliability and decrease development
time. [Code](http://en.wikipedia.org/wiki/Code_reuse)

**Separation of Concerns** - Different areas of functionality should be
managed by distinct and minimally overlapping modules of code.
[concern](http://en.wikipedia.org/wiki/Separation_of_concerns)

**Embrace Change** - This is the subtitle of a book by Kent Beck, and is
also considered a tenet of extreme programming and the agile methodology
in general. Many other principles are based on the concept that you
should expect and welcome change. In fact very old software engineering
principles like minimizing coupling are related directly to the
requirement of making code easier to change. Whether or not you are an
extreme programming practitioner, this approach to writing code just
makes sense. http://www.amazon.com/gp/product/0321278658


# Reflection

Is the ability of a computer program to **examine**(type introspection)
and **modify** the structure and behavior(specifically the values, meta-
data, properties and functions) of the program at runtime.

# Master a language

- Use language as much as you can. Make many things from this language.
  Make it fun.
- Read the docs about language: best practice, API, frameworks, design
  pattern, books
- Read other people's code and improve this.
- Support your code - every bug becomes a tour of your worst decisions.
- Learn a very different paradigm

# List of programming sites

https://www.reddit.com/r/cscareerquestions/comments/2luczb/are_coding_competition_sites_like_codechef/

In no particular order:
Topcoder - Programming Contests, Software Development, and Employment Services at TopCoder (http://topcoder.com/tc)
Codeforeces - Codeforces (http://codeforces.com/)
1. Codechef - Programming Competition,Programming Contest,Online Computer Programming (http://codechef.com/)
2. SPOJ - Sphere Online Judge (SPOJ) (http://spoj.pl/)
3. UVa - UVa Online Judge - Home (http://uva.onlinejudge.org/)
4. ProjectEuler - Project Euler (http://projecteuler.net/)
5. Programming Challenges -  Programming Challenges (http://programmingchallenges.com/)
6. ahmed-aly -  Virtual Online Contests (http://ahmed-aly.com/)
7. TJU -  TJU ACM-ICPC Online Judge (http://acm.tju.edu.cn/toj/)
8. PJU - UNION PANAMERICANA DE JUDO (http://pju.org/)
9. USACO -  USACO Training Program Gateway (http://ace.delos.com/usacogate)
10. TIMUS - Timus Online Judge (http://acm.timus.ru/)
11. AIZU - Programming Challenge (http://judge.u-aizu.ac.jp/onlinejudge/)
12. URI - URI Online Judge - Login (http://www.urionlinejudge.com.br/)
13. ZOJ - ZOJ :: Home (http://acm.zju.edu.cn/)
14. NTHU - NTHU Online Judge (http://acm.twbbs.org/)
15. Leetcode - LeetCode (http://leetcode.com/)
16. AI Challenge - Home | AI Challenge (http://aichallenge.org/)
17. Saratov - Saratov State University :: Online Contester (http://acm.sgu.ru/)
18. Google code jam - Google Code Jam (http://code.google.com/codejam)
19. InterviewStreet - Programming Contests - Codesprints - Interviewstreet (http://interviewstreet.com/)
20. Kaggle - making data science a sport (http://kaggle.com/)
21. Herbert - Welcome to Herbert Online Judge (http://herbert.tealang.info/)
22. CoderCharts - CoderCharts - Social Meets Programming (http://codercharts.com)
23. PKU - Welcome To PKU JudgeOnline (http://poj.org/)
24. CodingBat - CodingBat (http://codingbat.com/)
25. Programr - Programr | Learn.Code.Share (http://www.programr.com/)
26. HackerRank - Artificial Intelligence Challenges :: AI Programming Problems and Competitions :: HackerRank (https://www.hackerrank.com/)
27. Al Zimmermann - Al Zimmermann's Programming Contests (http://www.azspcs.net/)
28. Light OJ- Page on lightoj.com (http://www.lightoj.com/index.php)

# References

[wiki]: https://en.wikipedia.org/wiki/Computer_programming
[programming-language-wiki]: https://en.wikipedia.org/wiki/Programming_language
[Thoughts on programming]: https://github.com/Dobiasd/articles
[Devdocs.io]: https://github.com/Thibaut/devdocs
[Graph of reddit's words]: https://github.com/Dobiasd/programming-language-subreddits-and-their-choice-of-words

