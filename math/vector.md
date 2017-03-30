[TOC]

# Overview

- Vectors play a role in nearly all areas of mathematics and its
  applications.
- In physical settings, they are used to represent quantities that have
  both magnitude and direction, such as velocity and force.
    + Newtonian mechanics, quantum physics, and special and general re-
      lativity all depend fundamentally on vectors.
    + We could not understand electricity and magnetism without vectors,
      which are used in constructing the theoretical framework.
- Vectors also play a critical role in computer graphics, describing how
  light should be depicted, and providing a means to change the
  viewpoint of the screen appropriately.
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

# Dot Product and the Angle Between Two Vectors

## Definition

The dot product \\(\mathbf{v} \cdot \mathbf{w}\\) of two vectors
\\(\mathbf{v} = \langle v_1, v_2, v_3 \rangle, \mathbf{w} = \langle w_1,
w_2, w_3 \rangle\\) is the scalar defined by
\\[\mathbf{v \cdot w} = v_1w_1 + v_2w_2 + v_3w_3\\]

## Properties

i) \\(\mathbf{0 \cdot v = v \cdot 0 = 0}\\)
ii) Commutativity: \\(\mathbf{v \cdot w = w \cdot v}\\)
iii) Pulling out scalars: \\(\mathbf{(\lambda v)\cdot w = v\cdot
(\lambda w) = \lambda(v\cdot w)}\\)
iv) Distributive Law: \\(\mathbf{u\cdot(v+w) = u\cdot v+u\cdot w}\\)
v) Relation with length: \\(\mathbf{v\cdot v = \lVert v \rVert^2}\\)

## The Angle Between Two Vectors

- The angle between two vectors is chosen to satisfy
  \\(0\leq\theta\leq\pi\\).
- Let \\(\theta\\) be the angle between two nonzero vectors **v** and
**w**. Then
\\[\mathbf{v\cdot w = \lVert v \rVert\lVert w \rVert\cos\theta} \ or \
\mathbf{\cos\theta = \frac{v\cdot w}{\lVert v \rVert\lVert w \rVert}}\\]
- \\(\mathbf{v\perp w}\\) if and only if \\(\mathbf{v\cdot w = 0}\\)
- The angle \\(\theta\\) between **v** and **u** is obtuse if
  \\(\mathbf{v\cdot u}<0\\)

## Projection

Assume \\(\mathbf{v\neq0}\\). The **projection** of **u** along **v** is
the vector
\\[\mathbf{u_{\parallel v} = \left(\frac{u\cdot v}{v\cdot v}\right)v
= \left(\frac{u\cdot v}{\lVert v \rVert}\right)e_v}\\]
This is sometimes denoted \\(proj_{\mathbf{v}}\mathbf{u}\\).

The scalar \\(\mathbf{\frac{u\cdot v}{\lVert v \rVert}}\\) is called the
**component** or the **scalar component** of **u** along **v** and is
sometimes denoted \\(compj_{\mathbf{v}}\mathbf{u}\\).

## Decomposition

\\[\mathbf{u_{\perp v} = u - u_{\parallel v}}\\]
\\[\mathbf{u = u_{\parallel v} + u_{\perp v}}\\]

# The Cross Product

The cross product (vector product) is used in physics and engineering to
describe quantities involving rotation, such as torque and angular mo-
mentum. In electromagnetic theory, magnetic forces are described using
cross products.

Unlike the dot product \\(\mathbf{v\cdot w}\\) (which is a scalar), the
cross product \\(\mathbf{v\times w}\\) is again a vector. It is defined
using **determinants**
\\[
\begin{vmatrix}
a&b\\\\
c&d\\\\
\end{vmatrix}
= ad - bc
\\]

## Determinant

The determinant of a \\(3\times 3\\) matrix is defined by the formula
\\[
\begin{vmatrix}a_1&b_1&c_1\\\\a_2&b_2&c_2\\\\a_3&b_3&c_3\end{vmatrix}
= a_1\begin{vmatrix}b_2&c_2\\\\b_3&c_3\end{vmatrix} -
b_1\begin{vmatrix}a_2&c_2\\\\a_3&c_3\end{vmatrix} +
c_1\begin{vmatrix}a_2&b_2\\\\a_3&b_3\end{vmatrix}
\\]
This formula expresses the \\(3\times 3\\) determinant in terms of \\
(2\times 2\\) determinants called **minors**. The minors are obtained by
crossing out the first row and one of the three columns of the
\\(3\times 3\\) matrix.

## Definition

The cross product of vectors \\(\mathbf{v}=\langle v_1, v_2, v_3
\rangle\\) and \\(\mathbf{w}=\langle w_1, w_2, w_3 \rangle\\) is the
vector
\\[\mathbf{v\times w} = \begin{vmatrix}
\mathbf{i}&\mathbf{j}&\mathbf{w}\\\\
v_1&v_2&v_3\\\\
w_1&w_2&w_3\end{vmatrix} =
\begin{vmatrix}v_2&v_3\\\\w_2&w_3\end{vmatrix}\mathbf{i} -
\begin{vmatrix}v_1&v_3\\\\w_1&w_3\end{vmatrix}\mathbf{j} +
\begin{vmatrix}v_1&v_2\\\\w_1&w_2\end{vmatrix}\mathbf{k}
\\]

Using right-hand rule to determine the direction of the new vector.

## Theorem 1

i) \\(v\times w\\) is orthogonal to **v** and **w**
ii) \\(v\times w\\) has length \\(\lVert v \rVert\lVert w
\rVert\sin\theta\\) (\\(\theta\\) is the angle between **v** and **w**,
\\(0\leq\theta\leq\pi\\)).
iii) \\(\mathbf{\\{v,w,v\times w\\}}\\) forms a right-handed system.

## Properties

i) Anticommutative: \\(\mathbf{w\times v = -v\times w}\\)
ii) \\(\mathbf{v\times v=0}\\)
iii) \\(\mathbf{v\times w=0}\\) if and only if \\(\mathbf{w=\lambda
v}\\) for some scalar \\(\lambda\\) or **v = 0**.
iv) \\(\mathbf{(\lambda v)\times w=v\times(\lambda w)=\lambda(v\times
w)}\\)
v) \\(\mathbf{(u+v)\times w=u\times w+v\times w}\\)

## Cross Product, Area, and Volume

If \\(\mathcal{P}\\) is the parallelogram spanned by **v** and **w**,
and \\(\mathcal{T}\\) is the triangle spanned by **v** and **w**, then
\\[Area(\mathcal{P})=\mathbf{\lVert v\times w\rVert}\\]
\\[Area(\mathcal{T})=\mathbf{\frac{\lVert v\times w\rVert}{2}}\\]

Volume via Cross Products and Determinants: Let **u,v,w** be nonzero
vectors in \\(\mathbf{R}^3\\). Then the parallelepiped **P** spanned by
**uv,v,w** has volume
\\[V=\left|\mathbf{u\cdot(v\times w)}\right|=\left|det\begin
{pmatrix}\mathbf{u}\\\\\mathbf{v}\\\\\mathbf{w}\end{pmatrix}\right|\\]

# Planes in 3-Space

## Equation of a Plane

Plane through \\(P_0 = (x_0, y_0, z_0)\\) with normal vector \\(\mathbf
{n}=\langle a, b, c \rangle\\):
**Vector form:** \\(\mathbf{n}\cdot\langle x, y, z \rangle = d\\)

**Scalar forms:** \\(a(x-x_0)+b(y-y_0)+c(z-z_0)=0\\)
\\[ax+by+cz=d\\]
where \\(d=ax_0+by_0+cz_0\\)

A family of parallel planes is obtained by choosing a normal vector \\
(\mathbf{n}=\langle a, b, c \rangle\\) and varying the constant *d* in
the equation: \\(ax+by+cz=d\\). The unique plane in this family through
the origin has equation \\(ax+by+cz=0\\).

Points that lie on a same line are called **collinear**. If we given
three points P, Q, and R that are not collinear, then there is just one
plane passing through P, Q, and R.

# A Survey of Quadric Surfaces

Quadric surfaces are the surfaces analogs of conic sections. A conic
section is a curve in \\(\mathbf{R}^2\\) defined by a quadratic equation
in two variables. A quadric surface is defined by a quadratic equation
in **three** variables.
\\[Ax^2+By^2+Cz^2+Dxy+Eyz+Fyz+ax+by+cz+d=0\\]

When the coordinate axes are chosen to coincide with the axes of the
quadric, the equation of the quadric has a simple form. The quadric is
said to be in **standard position**
    - The coefficients D, E, F are all zero and the linear part
      \\(ax+by+cz+d\\) also reduces to just the constant term d.

## Ellipsoid

The surface analogs of ellipses are the egg-shaped **ellipsoids**.
\\[\left(\frac{x}{a}\right)^2+\left(\frac{y}{b}\right)^2+\left(\frac{z}
{c}\right)^2=1\\]

For a = b = c, this equation is equivalent to \\(x^2+y^2+z^2=a^2\\) and
the ellipsoid is a sphere of radius a.

Surfaces are often represented graphically by a mesh of curves called
**traces**, obtained by intersecting the surface with planes parallel to
one of the coordinate planes, yielding certain cross sections of the
surface. Algebraically, this corresponds to **freezing** one of the
three variables (holding it constant)

## Hyperboloid

The analogs of the hyperbolas are the **hyperboloid**, which come in two
types, depending on whether the surface has one or two components. We
refer to these types as hyperboloids of one or two sheets.
\\[One\ Sheet: \left(\frac{x}{a}\right)^2+\left(\frac{y}
{b}\right)^2=\left(\frac{z}{c}\right)^2+1\\]
\\[Two\ Sheets: \left(\frac{x}{a}\right)^2+\left(\frac{y}
{b}\right)^2=\left(\frac{z}{c}\right)^2-1\\]

Notices that a hyperboloid of two sheets does not contain any points
whose z-coordinate satisfies **-c < z < c** because the right-hand side
\\(\left(\frac{z}{c}\right)^2-1\\) is then negative, but the left-hand
side of the equation is greater than or equal to zero.

**Elliptic cone**
\\[\left(\frac{x}{a}\right)^2+\left(\frac{y}{b}\right)^2=\left(\frac{z}{
c}\right)^2\\]

An elliptic cone may be thought of as a limiting case of a hyperboloid
of one sheet in which we "pinch the waist" down to a point.

## Paraboloid

There are two types of paraboloid: elliptic and hyperbolic
\\[Elliptic: z=\left(\frac{x}{a}\right)^2+\left(\frac{y}{b}\right)^2\\]
\\[Hyperbolic: z=\left(\frac{x}{a}\right)^2-\left(\frac{y}
{b}\right)^2\\]

# Cylindrical and Spherical Coordinates

Two generalizations of polar coordinates to \\(\mathbf{R}^3\\):
cylindrical and spherical coordinates.

