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

# Vectors in Three Dimensions

The three-dimensional coordinate system satisfies the right-hand rule,
which means that when you position your right hand so that your fingers
curl from the positive x-axis toward the positive y-axis, your thumb
points in the positive z-direction.

Each point in space has unique coordinates \\((a,b,c)\\).

### Coordinate Planes

The **coordinate planes** in \\(R^3\\) are defined by setting one of the
coordinates equal to zero.
- The xy-plane consists of the points \\((a,b,0)\\) and is defined by
the equation \\(z=0\\).
- yz-plane: \\((0,b,c)\\) and \\(x=0\\)
- xz-plane: \\((a,0,c)\\) and \\(y=0\\)

The coordinate planes divide \\(R^3\\) into eight octants (analogous to
the four quadrants in the plane)
- The set of points \\((a,b,c)\\) with \\(a,b,c > 0\\) is called the
first octant.

### Distance Formula

The distance between \\(P=(a_1,b_1,c_1)\\) and \\(Q= (a_2,b_2,c_2)\\)
\\[\left| P-Q \right| = \sqrt{(a_2-a_1)^2+(b_2-b_1)^2+(c_2-c_1)^2}\\]

### Equations of Spheres and Cylinders

An equation of the sphere in \\(R^3\\) of radius R centered at \\(Q=
(a,b,c)\\) is
\\[(x-a)^2+(y-b)^2+(z-c)^2=R^2\\]
An equation of the right circular cylinder in \\(R^3\\) of radius R
whose central axis is the vertical line through \\((a,b,0)\\) is
\\[(x-a)^2+(y-b)^2=R^2\\]

### Addition and Scalar Multiplication

\\[\lambda v = \lambda\langle v_1,v_2,v_3 \rangle = \langle\lambda v_1,
\lambda v_2, \lambda v_3 \rangle\\]

\\[v+w = \langle v_1, v_2, v_3 \rangle + \langle w_1, w_2, w_3 \rangle
= \langle v_1+w_1, v_2+w_2, v_3+w_3 \rangle\\]

### Standard basis vectors

**i** = \\(\langle 1, 0, 0 \rangle\\), **j** = \\(\langle 0, 1, 0
\rangle\\), **k** = \\(\langle 0, 0, 1 \rangle\\)

Every vector is a linear combination of the standard basis vectors:

\\[\langle a, b, c \rangle = a\langle 1, 0, 0 \rangle + b\langle 0, 1,
0 \rangle + c\langle 0, 0, 1 \rangle = a\mathbf{i} + b\mathbf{j} +
c\mathbf{k}\\]

### Parametric Equations of a Line

A lien in \\(R^2\\) is defined by a single linear equation such as \\
(y=mx+b\\). In \\(R^3\\), a single linear equation defines a plane
rather than a line. We describe lines in \\(R^3\\) in parametric form.

Equation of a line (point-direction form) the line through \\(P_0 =
(x_0, y_0, z_0)\\) the direction of \\(\mathbf{v} = \langle a,b,c
\rangle\\) is described by

**Vector parametrization**
\\[\mathbf{r}(t) = \mathbf{r}_0 + t\mathbf{v} = \langle x_0,y_0,z_0
\rangle + t\langle a,b,c \rangle\\]
where \\(\mathbf{r}_0 = \vec{OP_0}\\)

**Parametric equations**
\\[x=x_0+at, y=y_0+bt, z=z_0+ct\\]
The parameter t takes on values \\(-\infty < t < \infty\\)
