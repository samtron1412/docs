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

## Resources

### List of programming sites

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

# Aspects of Computer Programming

## Quality Requirements

### Reliability

- How often the results of a program are correct.
- This depends on:
    + Conceptual correctness of algorithms, and
    + Minimization of programming mistakes
        * mistakes in resource management (e.g., buffer overflows and
          race conditions) and
        * logic errors (e.g., division by zero or off-by-one errors)

### Robustness

- How well a program anticipates problems due to errors (not bugs).
- This includes:
    + incorrect, inappropriate or corrupt data
    + unavailability of needed resources such as memory, operating
      system services and network connections
    + user error
    + unexpected power outages.

### Usability

- The ergonomics of a program: the ease with which a person can use the
  program for its intended purpose or in some cases even unanticipated
  purposes.
- This involves:
    + textual, graphical and sometimes hardware elements that improve
      the clarity, intuitiveness, cohesiveness and completeness of a
      program's user interface.

### Portability

- The range of computer hardware and operating system platform on which
  the source code of a program can be compiled/interpreted and run.

### Maintainability

- The ease with which a program can be modified by its present or future
  developers in order to make improvements or customizations, fix bugs
  and security holes, or adapt it to new environments.
- Readability of source code
    + Following a consistent programming style.
    + Comments
    + Naming conventions

### Efficiency/performance

- Measure of system resources a program consumes (processor time, memory
  space, slow devices such as disk, network bandwidth and to some extent
  even user interaction)
- The less, the better.
- This also includes careful management of resources, for example
  cleaning up temporary files and eliminating memory leaks.
- Algorithmic complexity: Big O notation

## Methodologies

- Software development processes
    + Agile software development
- Use Case analysis
- Object-Oriented Analysis and Design (OOAD) and Model-Driven
  Architecture (MAD): Unified Modeling Language (UML) is a notation used
  for both the OOAD and MDA.
- Database design: Entity-Relationship Modeling (ER Modeling)

## Testing - Debugging

Testing and create a bug report

Debugging:
- First, attempting to reproduce the problem.
- Second, simplifying the input of the program may need to make it
  easier to debug.
- Third, using debuggers.
- Fourth, fixing.
- Fifth, testing.

# Programming Paradigm

- Programming paradigms are a way to classify programming languages
  based on their features.
- Languages can be classified into multiple paradigms.
- Some paradigms are concerned mainly with implications for the
  execution model of the language, such as allowing side effects, or
  whether the sequence of operations is defined by the execution model.
- Other paradigms are concerned mainly with the way that code is
  organized, such as grouping a code into units along with the state
  that is modified by the code.
- Yet others are concerned mainly with the style of syntax and grammar.

## Common Programming Paradigms

- Imperative: which allows side effects
- Functional: which disallows side effects
- Declarative: which does not state the order in which operations
  execute
- Object-oriented: which groups code together with the state the code
  modifies
- Procedural: which group code into functions
- Logic: which has a particular style of execution model coupled to a
  particular style of syntax and grammar
- Symbolic: which has a particular style of syntax and grammar.

# Programming Languages

- A programming language is a formal language that specifies a set of
  instructions that can be used to produce various kinds of output.
- Different programming languages support different styles of
  programming (programming paradigms).
- The choice of language used is subject to many considerations:
    + commercial or free (license)
    + suitability to task
    + availability of third-party packages
    + programmers
    + compilers
    + efficiency

## Basic instructions

- Input: gather data from the input devices.
- Output: send data to the output devices.
- Arithmetic: perform basic arithmetical operations.
- Conditional Execution: check for certain conditions and execute the
  appropriate sequence of statements.
- Repetition: perform some action repeatedly.

## History

- First-generation programming languages (1GL)
    + Machine language: binary forms
    + Punched cards, magnetic tapes
- 1940s: Second generation (2GL)
    + Assembly languages
- 1950s: Third generation (3GL)
    + 1954: FORTRAN (John Backus)
    + 1959: COBOL (business use)
- 1960s - 1970s: Refinement
    + APL (1964)
        * Introduced array programming
        * Influenced functional programming
    + ALGOL (1958): refined structured procedural programming
    + Lisp (1958): the first dynamically typed functional programming
      language.
    + Simula (1965): the first language designed to support OOP.
    + Smalltalk(1972): the first purely OOP language.
    + C (1973): a system programming language
    + Prolog (1972): the first logic programming language
    + ML (1973) built a polymorphic type system on top of Lisp,
      pioneering statically typed functional programming language.
- 1980s: Consolidation and Growth
    + C++ (1980)
    + MATLAB (1984)
    + Objective-C (1986)
    + Perl (1987)
- 1990s: The Internet age
    + Rapid Application Development (RAD) language emerged, which
      usually came with an IDE, garbage collector. All were OOP
      languages.
    + Scripting languages
    + Haskell (1990)
    + Python (1991)
    + Visual Basic (1991)
    + Ruby (1993)
    + Lua (1993)
    + R (1993)
- Current trends
    + Increasing support for functional programming
    + Construct to support concurrent and distributed programming
    + Mechanism for adding security and reliability verification to the
      language: extended static checking, dependent typing, information
      flow control, static thread safety.
    + Alternative mechanisms for composability a modularity: mixins,
      traits, delegates, aspects.
    + Metaprogramming, reflection or access to the abstract syntax tree
    + Early research into quantum computing programming languages.
    + ActionScript (2000)
    + C# (2001)
    + Apache Groovy (2003)
    + Scala (2003)
    + F# (2005)
    + Windows PowerShell (2006)
    + Clojure (2007)
    + Go (2009)
    + Rust (2010)
    + Dart (2011)
    + Kotlin (2011)
    + TypeScript (2012)
    + Swift (2014)

## Elements

### Syntax

- The syntax of a computer language is the set of rules that defines the
  combinations of symbols that are considered to be a correctly
  structured document or fragment in that language.

#### Levels of syntax

- Computer language syntax is generally distinguished into three levels:
    + Words - the lexical level, determining how characters form tokens;
    + Phrases - the grammar level, determining how tokens form phrases;
    + Context - determining what objects or variables names refer to, if
      types are valid, etc.
- Distinguishing in this way yields modularity, allowing each level to
  be described and processed separately, and often independently.
    + First, a lexer turns the linear sequence of characters into a
      linear sequence of tokens; this is known as *lexical analysis* or
      *lexing*.
    + Second, the parser turns the linear sequence of tokens into a
      hierarchical syntax tree; this is known as *parsing*.
        * The first phase is the parse tree or *concrete syntax tree*
          which is determined by the grammar, but is generally far too
          detailed for practical use.
        * The second phase is the abstract tree (AST), which simplifies
          the concrete syntax tree into a usable form.
    + Finally, the contextual analysis resolves names and checks types.
    + Many languages an earlier step depends on a later step.
    + The AST and contextual analysis steps can be considered a form of
      semantic analysis, as they are adding meaning and interpretation
      to the syntax, or alternatively as informal, manual
      implementations of syntactical rules that would be difficult or
      awkward to describe or implement formally.
- The levels generally correspond to levels in the [Chomsky
  hierarchy][chomsky].
    + Words are in a regular language, specified in the lexical grammar,
      which is a Type-3 grammar, generally given as regular expressions.
    + Phrases are in a context-free language (CFL), generally a
      deterministic context-free language (DCFL), specified in a phrase
      structure grammar, which is a Type-2 grammar, generally given as
      production rules in Backus-Naur form (BNF).

### Semantics

- The term *semantics* refers to the meaning of languages, as opposed to
  their form (syntax).

### Type System

- A type system defines how a programming language classifies values and
  expressions into types, how it can manipulate those types and how they
  interact.
- The goal of a type system is to verify and enforce a certain level of
  correctness in programs written in that language by detecting certain
  incorrect operations.

#### Typed versus untyped language

- In the point of view of type theory, a language is typed if the
  specification of every operation defines types of data to which the
  operation is applicable, with the implication that it is not
  applicable to other types.
    + In practice, while few languages are considered typed, most modern
      languages offer a degree of typing.
    + The invalid operation may be detected when the program is compiled
      (static type checking) and will be rejected by the compiler with a
      compilation error message, or
    + It may be detected when the program is run (dynamic type
      checking), resulting in a run-time exception.
- A special case of typed languages are the single-type languages.
    + These are often scripting or markup languages, such as REXX or
      SGML.
    + They have only one data type - most commonly character strings
      which are used for both symbolic and numeric data.
- In contrast, an untyped language, such as most assembly languages,
  allows any operation to be performed on any data, which are generally
  considered to be sequences of bits of various lengths.
    + High-level languages which are untyped include BCPL, Tcl, etc.

#### Static versus dynamic typing

- Statically typed languages can be either manifestly typed or type-
  inferred.
    + Manifestly typed: the programmer must explicitly write types at
      certain textual positions (for example, at variable declarations).
        * C++, C#, Java
    + Type-inferred: the compiler infers the types of expressions and
      declarations based on context.
        * Haskell, ML
- Dynamic typing determines the type-safety of operations at run time;
  types are associated with run-time values rather than textual
  expressions.
    + It does not require the programmer to write explicit type
      annotations on expressions.
    + It permits a single variable to refer to values of different types
      at different points in the program execution.
    + Lisp, Smalltalk, Perl, Python, JavaScript, Ruby

#### Weak and strong typing

- Weak typing allows a value of one type to be treated as another, for
  example treating a string as a number.
- Strong typing prevents the above. An attempt to perform an operation
  on the wrong type of value raises an error. Strongly typed languages
  are often termed type-safe or safe.

### Standard Library And Run-Time System

- Most programming languages have an associated core library (sometimes
  known as the "standard library", especially if it is included as part
  of the published language standard), which is conventionally made
  available by all implementations of the language.
    + Core libraries typically include definitions for commonly used
      algorithms, data structures, and mechanisms for input and output.

## Design and Implementation

- Programming languages share properties with natural languages related
  to their purpose as vehicles for communication, having a syntactic
  form separate from its semantics, and showing language families of
  related languages branching one from another.
- But as artificial constructs, they also differ in fundamental ways
  from languages that have evolved through usage.
    + A significant difference is that a programming language can be
      fully described and studied in its entirety, since it has a
      precise and finite definition. By contrast, natural languages have
      changing meanings given by their users in different communities.
    + Natural languages lack the precise and complete semantic
      definition that a programming language has.
- The need for diverse programming languages arises from the diversity
  of contexts in which languages are used:
    + Programs range from tiny scripts written by individual hobbyists
      to huge systems written by hundreds of programmers.
    + Programmers range in expertise from novices, who need simplicity
      above all else, to experts who may be comfortable with
      considerable complexity.
    + Programs must balance speed, size, and simplicity on systems
      ranging from microcontrollers to supercomputers.
    + Programs may be written once and not change for generations, or
      they may undergo continual modification.
    + Programmers may simply differ in their tastes: they may be
      accustomed to discussing problems and expressing them in a
      particular language.
- One common trend in the development of programming languages has been
  to add more ability to solve problems using a higher level of
  abstraction.
    + The earliest programming languages were tied very closely to the
      underlying hardware of the computer.
    + As new programming languages have developed, features have been
      added that let programmers express ideas that are more remote from
      simple translation into underlying hardware instructions.
    + Because programmers are less tied to the complexity of the
      computer, their programs can do more computing with less effort
      from the programmer. This lets them write more functionality per
      time unit.

### Specification

- The specification of a programming language is an document that the
  language users and the implementers can use to agree upon whether a
  piece of source code is valid program in that language, and if so what
  its behavior shall be.
- A programming language specification can take several forms, including
  the following:
    + An explicit definition of the syntax, static semantics, and
    execution semantics of the language.
        * While syntax is commonly specified using a formal grammar,
          semantic definitions may be written in natural language (C
          language), or a formal semantics (ML, Scheme).
    + A description of the behavior of a translator for the language
      (e.g., the C++ and Fortran specifications). The syntax and
      semantics of the language have to be inferred from this
      description, which may be written in natural or a formal language.
    + A reference or model implementation, sometimes written in the
      language being specified (Prolog or ANSI REXX). The syntax and
      semantics of the language are explicit in the behavior of the
      reference implementation.

### Implementation

- An implementation of a programming language provides a way to write
  programs in that language and execute them on one or more
  configurations of hardware and software.
- There are two approaches to programming language implementation:
  *compilation* and *interpretation*.
    + One technique for improving the performance of interpreted program
      is just-in-time compilation.
            * Here the virtual machine, just before execution,
              translates the blocks of bytecode which are going to be
              used to machine code, for direct execution on the
              hardware.

## Mastering a programming language

- Use language as much as you can. Make many things from this language.
  Make it fun.
- Read the docs about language: best practice, API, frameworks, design
  pattern, books
- Read other people's code and improve this.
- Support your code - every bug becomes a tour of your worst decisions.
- Learn a very different paradigm

# Principles of Good Programming

## Code tells you HOW, comments tell you WHY

- https://blog.codinghorror.com/code-tells-you-how-comments-tell-you-why/
- literature programming
- programmers first, compiler second
- Code tells you HOW, comments tell you WHY

## Others

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

# Program life-cycle phase

- Program life cycle phases are the stages a computer program undergoes,
from initial creation to deployment and execution.
- The phases are: edit time, compile time, distribution time,
installation time, link time, load time, and run time.
- Life-cycle phases do not necessarily happen in a linear order, and
they can be intertwined in various ways.

## Edit time (or Design time)

Edit time is when the source code of the program is being edited.
- Bug fix, refactoring, or addition of new features.

## Compile time

Compile time is when source code is translated into machine code by a
compiler.
- Language checking

## Distribution time

- Distribution time is process of transferring a copy of a program to a
user.

## Installation time

Installation time gets the distributed program ready for execution on
the user's computer.

## Link time

Link time connects all of the necessary machine code components of a
program, including externals.
- Static linking: the connection is made by the compiler, which is
always prior to execution.
- Dynamic linking: the OS does this just before, or even during
execution.

## Load time

When the OS takes the program's executable from storage, and places it
into active memory, in order to begin execution.

## Run time

Run time is the execution phase, when the central processing unit
executes the program's machine code instructions.
- Programs may run indefinitely until a normal termination or a crash.

# General concepts

## Runtime system

### Notable runtimes

#### Android Runtime (ART)

#### Common Language Runtime (CLR)

#### Java Virtual Machine (JVM)

#### Node.js

#### crt0

#### Zend Engine

## Runtime library

## Executable

## Compiler

### Compilation strategies

#### Just-in-time (JIT)

#### Ahead-of-time (AOT)

#### Transcompilation

#### Recompilation

## Interpreter

## Virtual machine

## Intermediate representation (IR)

## Source code

## Object code

## Bytecode

## Machine code


## Thread safety (threadsafe)

### Introduction

- Thread safety is a computer programming concept applicable to multi-
  threaded code.
    + Thread-safe code only manipulates shared data structures in a
      manner that ensures that all threads behave properly and fulfill
      their design specifications without unintended interaction.
    + Synchronization

### Levels of thread safety

- Software libraries can provide certain thread-safety guarantees
- Thread safe
    + implementation is guaranteed to be free of race conditions when
      accessed by multiple threads simultaneously.
- Conditionally safe
    + different threads can access different objects simultaneously, and
      access to shared data is protected from race conditions.
- Not thread safe
    + code should not be accessed simultaneously by different threads
- Thread safety guarantees usually also include design steps to prevent
  or limit the risk of different forms of deadlocks, as well as
  optimizations to maximize concurrent performance.
    + However, deadlock-free guarantees cannot always be given, since
      deadlocks can be caused by callbacks and violation of
      architectural layering independent to the library itself.

### Implementation Approaches

- Avoiding shared state
    + Re-entrancy
        * Writing code in such a way that it can be partially executed
          by a thread, reexecuted by the same thread or simultaneously
          executed by another thread and still correctly complete the
          original execution.
        * This requires the saving of state information in variables
          local to each execution, usually on a stack, instead of in
          static or global variables or other non-local state.
        * All non-local state must be accessed through atomic operations
          and the data-structures must also be reentrant.
    + Thread-local storage
        * Variables are localized so that each thread has its own
          private copy
    + Immutable objects
        * The state of an object cannot be changed after construction
- Synchronization-related
    + Mutual exclusion
        * Access to shared data is serialized using mechanisms that
          ensure only one thread reads or writes to the shared data at
          the time.
        * Improper usage can lead to side-effects like deadlocks,
          livelocks, and resource starvation.
    + Atomic operations
        * Shared data are accessed by using atomic operations which
          cannot be interrupted by other threads.
- Concurrent design
    + involves structuring the shared state in a manner that allows
      multiple threads to simultaneously modify the state without
      interfering with each other.

### Resources

- https://blogs.msdn.microsoft.com/ericlippert/2009/10/19/what-is-this-thing-you-call-thread-safe/

# Tools

- [Email][email]
- [git][git]
- [cgit][cgit]
- [patchwork][patchwork]: Patchwork is a web-based patch tracking system
  designed to facilitate the contribution and management of
  contributions to an open-source project.

# Programming Challenges

- Gaussian/Gauss-Jordan Elimination
- Finding the inverse of a matrix
- Finding the determinant of a matrix
- Quine: https://en.wikipedia.org/wiki/Quine_(computing)

# References

[wiki]: https://en.wikipedia.org/wiki/Computer_programming
[programming-language-wiki]: https://en.wikipedia.org/wiki/Programming_language
[syntax]: https://en.wikipedia.org/wiki/Syntax_(programming_languages)
[chomsky]: https://en.wikipedia.org/wiki/Chomsky_hierarchy
[Thoughts on programming]: https://github.com/Dobiasd/articles
[Devdocs.io]: https://github.com/Thibaut/devdocs
[Graph of reddit's words]: https://github.com/Dobiasd/programming-language-subreddits-and-their-choice-of-words
[software]: https://en.wikipedia.org/wiki/Software
[phases]: https://en.wikipedia.org/wiki/Program_lifecycle_phase
[patchwork]: http://jk.ozlabs.org/projects/patchwork/
[email]: https://en.wikipedia.org/wiki/Email
[git]: https://git-scm.com/
[cgit]: https://git.zx2c4.com/cgit/about/
[threadsafe]: https://en.wikipedia.org/wiki/Thread_safety
