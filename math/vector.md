[TOC]

# Overview

- Vectors play a role in nearly all areas of mathematics and its
applications.
- In physical settings, they are used to represent quantities that have
both magnitude and direction, such as velocity and force.
    + Newtonian mechanics, quantum physics, and special and general
    relativity all depend fundamentally on vectors.
    + We could not understand electricity and magnetism without vectors,
    which are used in constructing the theoretical framework.
- Vectors also play a critical role in computer graphics, describing how
light should be depicted, and providing a means to change the viewpoint
of the screen appropriately.
- Fields such as economics and statistics use vectors to encapsulate
information in a manner that provides for efficient manipulation.

# Vectors in the plane

- A two-dimensional vector **v** is determined by two
  points in the plane:
    + An initial point P (tail or basepoint)
    + A terminal point Q (head)

\\[\mathbf{v} = \vec{PQ}\\]

- The **length** or **magnitude** of **v**, denoted
  \\(\lVert\vec{\mathbf{v}}\rVert\\) is the distance from P to Q.
- The vector \\(\vec{\mathbf{v}} = \vec{OR}\\) pointing from the origin
to a point R is called the **position vector** of R.
- Two vectors **v** and **w** of nonzero length are called **parallel**
  if the lines through **v** and **w** are parallel.
- A vector **v** is said to undergo a **translation** when it is moved
  to begin at a new point without changing its length or direction. The
  resulting vector **w** is called a translate of **v**.
    + **v** and **w** are **equivalent** if **w** is a translate of
      **v**.
    + Every vector **v** is equivalent to a unique vector
    **v<sub>0</sub>** based at the origin.

## Definition: Components of a Vector

- The components of **v** = \\(\vec{PQ}\\), where \\(P=(a_1,b_1), Q=
  (a_2,b_2)\\), are the quantities
\\[a=a_2-a_1 (x-component), b=b_2-b_1 (y-component)\\]
The pair of components is denoted \\(\left\langle a,b \right\rangle\\).
- The length of a vector in terms of its components:
\\[\lVert\mathbf{v}\rVert = \lVert\vec{PQ}\rVert = \sqrt{a^2+b^2}\\]
- The **zero vector** (whose head and tail coincide) is the vector **0**
\\(= \langle 0,0 \rangle\\) of length zero. It is the only vector that
lacks a direction.
- The components \\(\langle a,b \rangle\\) determine the length and
direction of **v**, but not its basepoint. Therefore, two vectors are
equivalent if and only if they have the same components.

## Vector Algebra

### Vector Addition

- The vector sum **v + w** is defined when **v** and **w** have the same
basepoint: parallelogram law
    + `v - w = v + (-w)`

### Scalar Multiplication

- The term **scalar** is another word for **real number**.
- \\(\left|\lambda v \right| = \left|\lambda\right| \lVert v \rVert\\)
- It points in the same direction as **v** if \\(\lambda > 0\\).
- It points in the opposite direction if \\(\lambda < 0\\)

### Vector Operations Using Components

If **v** = \\(\langle a,b \rangle\\) and **w** = \\(\langle c,d
\rangle\\)

i) \\(v + w = \langle a+c, b+d \rangle\\)
ii) \\(v - w = \langle a-c, b-d \rangle\\)
iii) \\(\lambda v = \langle\lambda a,\lambda b\rangle\\)
iv) \\(v + 0 = 0 + v = v)

### Basic Properties of Vector Algebra

For all vectors **u, v, w** and for all scalars \\(\lambda\\)
- Commutative Law: \\(v+w=w+v\\)
- Associative Law: \\(u+(v+w)=(u+v)+w\\)
- Distributive Law for Scalars: \\(\lambda(v+w)=\lambda v+\lambda w\\)

### Linear Combination

A **linear combination** of vectors **v** and **w** is a vector:
\\[r\mathbf{v} + s\mathbf{w}\\]

### Conceptual Insight

In general, to write a vector as a **linear combination** of two other
vectors, we have to solve a system of two linear equations in two
unknowns variables. On the other hand, vectors give us a way to
visualizing the system of equations geometrically. This relation between
vectors and systems of linear equations extends to any number of
variables and is the starting point for the important subject of
**linear algebra**.

### Triangle Inequality

For any two vectors **v** and **w**,
\\[\lVert v+w \rVert \leq \lVert v \rVert + \lVert w \rVert\\]
Equality holds only if **v=0** or **w=0**, or if \\(w=\lambda v\\),
where \\(\lambda \geq 0\\).
