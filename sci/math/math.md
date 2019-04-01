[TOC]

# Overview

Mathematics (from Greek, "knowledge, study, learning") is the language
of universe and the natural basic science.

## Resources

### Books

- https://math.stackexchange.com/questions/69060/what-is-a-good-book-for-learning-math-from-the-ground-up
- https://www.goodreads.com/list/show/8231.Best_Books_About_Mathematics
- https://www.reddit.com/r/math/comments/2p2ggd/i_want_to_own_the_best_textbooks_for_all_of_math/
- https://math.stackexchange.com/questions/741132/good-book-for-mathematical-modeling
- https://www.math.ualberta.ca/mss/misc/A%20Mathematician's%20Apology.pdf

### Sites

- https://jeremykun.com/
- https://j2kun.svbtle.com/
- https://medium.com/@jeremyjkun
- mathinsight.org

### Online cources

- [Math As A Second Language][mathasasecondlanguage]
- [Classic Arithmetic][classicarithmetic]

### Software

- Sage: http://www.sagemath.org/
- Maxima: http://maxima.sourceforge.net/
- GNU Octave: https://www.gnu.org/software/octave/
- https://mathematica.stackexchange.com/questions/28162/alternatives-to-mathematica
- https://github.com/corywalker/expreduce
- https://alternativeto.net/software/mathematica/?license=free
- https://en.wikipedia.org/wiki/List_of_computer_algebra_systems

# History

## Etymology

# Definitions of Mathematics

## Normal definitions

- Mathematics is the study of topics such as quantity (numbers),
  structure, space, and change.

## Greater abstraction - Philosophical definitions

- Mathematics is the science that draws necessary conclusions.

# Inspiration and aesthetics


# Notation, language, and rigor

- Closed-form expression
    + https://en.wikipedia.org/wiki/Closed-form_expression
    + can be evaluated in a finite number of operations
    + It may contain constants, variables, certain "well-known"
      operations (e.g., + − × ÷), and functions (e.g., nth root,
      exponent, logarithm, trigonometric functions, and inverse
      hyperbolic functions), but usually no limit

# Fields of Mathematics

- Mathematics can be subdivided into the study of quantity, structure,
space, and change (i.e. arithmetic, algebra, geometry, and analysis).
- In addition to these main concerns, there are also subdivisions.

## Foundations

### Mathematical logic

Mathematical logic includes the mathematical study of logic and the
applications of formal logic to other areas of mathematics.

### Set theory

Set theory is the branch of mathematics that studies sets or collections
of objects.

### Category theory

Category theory, which deals in an abstract way with mathematical
structures and relationships between them, is still in development.

### Theory of computation

In theoretical computer science and mathematics, the theory of
computation is the branch that deals with how efficiently problems can
be solved on a model of computation, using an algorithm. The field is
divided into three major branches: automata theory and language,
computability theory, and computational complexity theory, which are
linked by the question: "What are the fundamental capabilities and
limitations of computers?"

## Pure mathematics

### Quantity - Arithmetic

Natural numbers, Integers, Rational numbers, Real numbers, Complex
numbers

### Structure

- Combinatorics
- Number theory
- Group theory
- Graph theory
- Order theory
- Algebra

### Space

- Geometry
- Trigonometry
- Differential geometry
- Topology
- Fractal geometry
- Measure theory

### Change

+ [Analysis vs. Calculus](https://math.stackexchange.com/questions/32433/are-calculus-and-real-analysis-the-same-thing)

- Analysis
    + Differential equations
- Calculus
- Dynamical systems
- Chaos theory

## Applied mathematics

- Mathematical physics
- Fluid dynamics
- Numerical analysis
- Optimization
- Probability theory
- Statistics
- Cryptography
- Mathematical finance
- Game theory
- Mathematical biology
- Mathematical chemistry
- Mathematical economics
- Control theory

# Proving - Problem solving - How to think

```
Remember, 16AB are fundamentally courses designed to help you think
better. They do so by demonstrating ways of thinking during lecture
(this is why actually attending lecture is helpful) and discussion, by
walking you through certain patterns of thought on homeworks (this is
why actually reading the entire problem is important), and by forcing
you to both extrapolate and interpolate what you have learned on the HW.

Anyway, at the surface level, this problem shows you how to prove the
uniqueness of the solutions of these kinds of differential equations.

More deeply, it hopefully has sparked a bit of awareness that indeed,
such a proof is actually required. Being able to think that way is
important. Incoming students often have a hard time distinguishing
between the true substance of rigor and proper thinking, and what some
might call "cargo cult rigor" (a la Feynman's colorful analogy). The
rituals of procedure are not what are important, it is the actual
grounding in justification. The proof of uniqueness of solutions is what
allows us to be flexible in how we guess solutions.

At a technical level, the thinking demonstrated in the statement of the
problem helps you see how a proof can often be derived by clearly
thinking step by step, and being willing to focus in on the easiest
cases first. Here, the x0≠0 is the easier case.

Then the willingness to consider what you know how to do (i.e. take a
ratio or a difference) and to consider the ingredients that you have
(i.e. you better have some approach that involves taking a derivative
since you only are given information about the derivative. Here, it is
the ability to accept that maybe you could've tried the difference, but
you probably would have gotten stuck. (You should try to go the
difference route for yourself. You'll see how you get stuck.) Seeing the
thought process written out is designed to help you be more comfortable
engaging in similar thought processes yourself.

Then, it is being willing to come back to the harder case of x0=0 that
seems obvious, but blocks the simple approach that worked in the easier
case. The problem next tries to demonstrate how you can think through
the process of thinking here, realizing that fundamentally, you want to
show impossibility of being different. And telling you that when you
feel that way, you might want to try to start with an argument by
contradiction.

The problem next demonstrates the micro-skill of writing out what
exactly it means for something not to be zero. This is a crucial step in
proofs by contradiction --- finding something in the false assumption to
grab hold of so you can unravel things.

The problem next shows that from here, you need to somehow drive towards
a contradiction. There are literally only two directions to go ---
forward in time or backwards in time. And one of them is aiming at
somewhere you have a given fact that you can hope to contradict, and the
other is going off to infinity. So you can choose to go towards zero.
(The fact that these kinds of simple decisions in proofs can be
navigated by just thinking calmly is what is being shown here.)

From there, the problem shows that you can leverage what you already
know. This idea of reducing to something that you do already understand
is a common theme across 16A and even 61A. It will be built upon even
more in 16B, and then plays a big role in 70 and then in 170 and 127,
and even 126 to an extent. In this particular case, we focus in on the
nonzero initial condition case for which uniqueness was already proved.

The problem closes with just how you take a proof to an actual
contradiction.

The whole proof is less than 10 lines total if written out without any
commentary but all work shown. The length of the problem is because it
is designed to help provide that "director's commentary" to help you
internalize how people can come up with this stuff. In a more advanced
course, we'd simply say "prove the uniqueness of this solution" and be
done with it. But this is 16B. The problems are longer because students
are less mature.

At the end of the day, the goal of your Berkeley education in to help
you be able to come up with new things in new situations. Providing you
with the full complement of thinking skills required to do that is what
questions are trying to do. Apprenticeship is about learning how the
master thinks while you do the tasks the master tells you to do. It is
about watching the master work and understanding why the master does
those things. This is what the homework, reading solutions, doing
self-grades, redoing problems, attending lecture, etc. are all doing, as
well as lab. We are trying to deconstruct approximate apprenticeship in
a scalable distributed way.
```

# Mathematical Model

- A mathematical model is a description of a system using mathematical
  concepts and language.
    + Mathematical models are used in the natural sciences such as
      physics, biology, chemistry, etc. and engineering disciplines such
      as computer science, as well as in the social sciences such as
      economics, psychology, sociology, political science.

# Unsolved problems

- https://en.wikipedia.org/wiki/List_of_unsolved_problems_in_mathematics

# Mathematical awards

- Arguably the most prestigious award in mathematics is the Fields
  Medal, established in 1936 and awarded every four years (except around
  World War II) to as many as four individuals.

# [Mathematical Philosophy](https://en.wikipedia.org/wiki/Philosophy_of_mathematics)

something

# References

[wiki-mathematics]: https://en.wikipedia.org/wiki/Mathematics
[mathworld]: http://mathworld.wolfram.com/
[wiki-philosophy]: https://en.wikipedia.org/wiki/Philosophy_of_mathematics
[wiki-millennium]: https://en.wikipedia.org/wiki/Millennium_Prize_Problems
[wiki-areas]: https://en.wikipedia.org/wiki/Areas_of_mathematics
[wiki-foundations]: https://en.wikipedia.org/wiki/Foundations_of_mathematics
[foundations]: http://mathworld.wolfram.com/topics/FoundationsofMathematics.html
[multivar]: http://mathinsight.org/thread/multivar
[khan-multivar]: https://www.khanacademy.org/math/multivariable-calculus
[how-to]: http://tutorial.math.lamar.edu/Extras/StudyMath/HowToStudyMath.aspx
[common-errors]: http://tutorial.math.lamar.edu/Extras/CommonErrors/CommonMathErrors.aspx
[wiki-calculus]: https://en.wikipedia.org/wiki/Calculus
[loop]: https://math.stackexchange.com/questions/1334678/does-mathematics-become-circular-at-the-bottom-what-is-at-the-bottom-of-mathema
[set-set]: https://math.stackexchange.com/questions/121128/when-does-the-set-enter-set-theory
[mathasasecondlanguage]: https://www.youtube.com/watch?v=QFFReY6lS68&list=PLufObkSlzUUU4oKivkiwchXBRfAzQXpcu&index=1
[classicarithmetic]: https://www.youtube.com/playlist?list=PL5Y01D9mNkO8PcdgTyLJYcVJo9O906tIy
