[TOC]

# Overview

- In machine learning and statistics, classification is the problem of
  identifying to which of a set of categories (sub-populations) a new
  observation belongs, on the basis of a training set of data containing
  observations (or instances) whose category membership is known.
- Examples are assigning a given email to the "spam" or "non-spam"
  class, and assigning a diagnosis to a given patient based on observed
  characteristics of the patient (gender, blood pressure, presence or
  absence of certain symptoms, etc.)
- Classification is an example of pattern recognition (machine learning).
- Classification is considered an instance of supervised learning, i.e.
  learning where a training set of correctly identified observations is
  available.
    + The corresponding unsupervised procedure is known as clustering,
      and involves grouping data into categories based on some measure
      of inherent similarity or distance.
- The individual observations are analyzed into a set of quantifiable
  properties, known as explanatory (independent) variables or features.
    + These properties may be categorical (e.g. "A", "B", "AB" or "O"
      for blood type), ordinal (e.g. "large", "medium", or "small"),
      integer-valued (e.g. the number of occurrences of a particular
      word in an email) or real-valued (e.g. a measurement of blood
      pressure)
- An algorithm that implements classification, especially in a concrete
  implementation, is known as a classifier.
    + The term classifier sometimes also refers to the mathematical
      function, implemented by a classification algorithm, that maps
      input data to a category.

# Probabilistic classification

- In machine learning, a probabilistic classifier is a classifier that
  is able to predict, given an observation of an input, a probability
  distribution over a set of classes, rather than only outputting the
  most likely class that the observation should belong to.
- It's useful when combining classifier into `ensembles`
    + Because of the probabilities which are generated, probabilistic
      classifiers can be more effectively incorporated into larger
      machine-learning tasks, in a way that partially or completely
      avoids the problem or `error propagation`
- Some classification models, such as naive Bayes, logistic regression
  and multilayer perceptrons (when trained under an appropriate loss
  function) are naturally probabilistic.
- Other models such as support vector machines are not, but methods
  exist to turn them into probabilistic classifiers.

# Frequentist procedures

Something

# Bayesian procedures

- Markov Chain Monte Carlo (MCMC)

# Statistical procedures

- Two procedures
    + Partitioning data into statistically different samples
    + Merging the samples which are similar according to the test
      statistics.
- The split/merge operations are repeated as long as data samples can be
  split until the maximum purity of classes is obtained.

# Binary classification

- https://en.wikipedia.org/wiki/Binary_classification
- classifying the elements of a given set into two groups
    + predicting which group each one belongs to
- contexts requiring a decision as to whether or not an item has some
  qualitative property, some specified characteristic
- some typical binary classification
    + medical testing to determine if a patient has certain disease or
      not => the classification property is "the presence of the
      disease"
    + A "pass or fail" test method or quality control in factories
    + Information retrieval, deciding whether a page or an article
      should be in the result set of a search or not => the
      classification property is "the relevance of the article, or the
      usefulness to the user"

# Multiclass classification

- https://en.wikipedia.org/wiki/Multiclass_classification


# Algorithms

## Linear classifiers

Something

# Evaluation

Something

# Application

Something

# References

