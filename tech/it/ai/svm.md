[TOC]

# Overview

- In machine learning, support vector machines (SVMs, also support
  vector networks) are
    + supervised learning models
    + with associated learning algorithms that analyze data used for
      classification and regression analysis.
    + it is a non-probabilistic binary linear classifier.
- An SVM model is
    + a representation of the examples as points in space
    + mapped so that the examples of the separate categories are divided
      by a clear gap that is as wide as possible
    + new examples are then mapped into that same space and predicted to
      belong to a category based on which side of the gap they fall
- In addition to performing linear classification, SVMs can efficiently
  perform a non-linear classification using what is called the kernel
  trick
    + implicitly mapping their inputs into high-dimensional feature
      spaces
- When data is unlabelled, supervised learning is not possible
    + an unsupervised learning approach is required, which attempts to
      find natural clustering of the data to groups, and then map new
      data to these formed groups
    + The `support vector clustering` algorithm created by Hava
      Siegelmann and Valdimir Vapnik, applies the statistics of support
      vectors, developed in the support vector machines algorithms, to
      categorize unlabelled data.

# History

Something

# Motivation

- Given data points each belong to one of two classes, and the goal is
  to decide which class a new data point will be in.
- The case of SVMs, a data point is viewed as a p-dimensional vector (a
  list of p numbers)
- And we want to know whether we can separate such points with a
  (p-1)-dimensional hyperplane. This is called a linear classifier.
    + There are many hyperplanes that might classify the data.
    + One reasonable choice as the best hyperplane is the one that
      represents the largest separation, or margin, between the two
      classes.
    + We choose the hyperplane so that the distance from it to the
      nearest data point on each side is maximized.
    + If such a hyperplane exists, it is known as the maximum-margin
      hyperplane and the linear classifier it defines is known as a
      maximum margin classifier, or equivalently, the perceptron of
      optimal stability

# Definition

- Formally, a SVM constructs a hyperplane or set of hyperplanes in a
  high- or infinite-dimensional space, which can be used for
  classification, regression, or other tasks like outliers detection.
- Intuitively, a good separation is achieved by the hyperplane that has
  the largest distance to the nearest training-data point of any class
  (so-called functional margin)
- Whereas the original problem may be stated in a finite dimensional
  space, it often happens that the sets to discriminate are not linearly
  separable in that space.
    + solution: the original finite-dimensional space be mapped into a
      much higher-dimensional space, presumably making the separation
      easier in that space.
    + to keep the computational load reasonable, the mappings used by
      SVM schemes are designed to ensure that dot products may be
      computed easily in terms of the variables in the original space,
      by defining them in terms of a kernel function k(x,y) selected to
      suit the problem.
    + the hyperplanes in the higher-dimensional space are defined as the
      set of points whose dot product with a vector in that space is
      constant.
    + the vectors defining the hyperplanes can be chosen to be linear
      combinations with parameters ai of images of feature vectors xi
      that occur in the data base.
    + with this choice of a hyperplane are defined by the relation

# Applications

Something

# Linear SVM

## Hard-margin

Something

## Soft-margin

Something

# Non-linear classification

Something

# Computing the SVM classifier

## Primal

Something

## Dual

Something

## Kernel trick

Something

## Sub-gradient descent

Something

## Coordinate descent

Something

# Empirical risk minimization

Something

# References

[wiki]: https://en.wikipedia.org/wiki/Support_vector_machine
