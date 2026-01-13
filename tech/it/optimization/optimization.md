# Overview

# Common concepts

- Simplex algorithm
    + https://en.wikipedia.org/wiki/Simplex_algorithm
    + Simplex
        * https://en.wikipedia.org/wiki/Simplex
        * Simplest possible polytope (geometric object with flat sides -
          faces) in any given dimension.
- Big M method
    + https://en.wikipedia.org/wiki/Big_M_method
    + In some software, they introduce `indicator constraints` to mimic
      the behavior of Big M method.
        * https://or.stackexchange.com/questions/231/when-to-use-indicator-constraints-versus-big-m-approaches-in-solving-mixed-int

# Algorithms

## Alternating Direction Method of Multipliers (ADMM)

The ADMM (Alternating Direction Method of Multipliers) algorithm is a
powerful technique for solving linearly constrained, convex optimization
problems, especially those where the objective function is a sum of two
or more functions that are easily solvable individually but coupled by a
constraint. It works by forming an augmented Lagrangian and then
iteratively updating the variables in an alternating fashion, first
solving for one set of variables (e.g., x), then the other (e.g., z),
and finally updating the Lagrange multipliers (λ) to satisfy the
constraint. This "splitting" approach allows for efficient solutions to
problems that would otherwise be difficult to solve, and it forms the
basis for more advanced methods, particularly in distributed
optimization and machine learning.
