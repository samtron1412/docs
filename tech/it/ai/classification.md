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
- Converting continuous values to binary
    + continuous values, such as blood values => defining a cutoff value
      => higher is positive and lower is negative
    + it can cause a loss of information

# Multiclass classification

- https://en.wikipedia.org/wiki/Multiclass_classification
- In machine learning, multiclass or multinomial classification is the
  problem of classifying instances into one of three or more classes.

## General strategies

### Transformation to binary

#### One-vs.-rest

Something

#### One-vs.-one

Something

### Extension from binary

#### Neural Networks

Something

#### k-nearest neighbors

Something

#### Naive Bayes

Something

#### Decision trees

Something

#### Support vector machines

Something

### Learning paradigms

Something


# Multi-label classification

- Multi-class classification and the strongly related problem of
  multi-output classification are variants of the classification problem
  where multiple labels may be assigned to each instance.
    + IT is a generalization of multiclass classification since it has
      no constraint on how many of the classes the instance can be
      assigned to.
- Formally, multi-label classification is the problem of finding a model
  that maps inputs X to binary vectors Y (assigning a value of 0 or 1
  for each element (label) in Y)

## Problem transformation methods

- Independently training one binary classifier for each label
    + this method of dividing the task into multiple binary tasks has
      something in common with the one-vs.-all (OvA) method for
      multiclass classification.

# Algorithms

## Linear classifiers

- A large number of algorithms for classification can be phrased in
  terms of a linear function that assigns a score to each possible
  category k by combining the feature vector of an instance with a
  vector of weights, using a dot product.
    + The predicted category is the one with the highest score
    + This type of score function is known as a linear predictor
      function and has the following general form
        * `score (Xi, k) = Bk . Xi`
        * where Xi is the feature vector for instance i
        * Bk is the vector of weights corresponding to category k
        * and score(Xi, k) is the score associated with assigning
          instance i to category k
- Algorithms with this basic setup are known as linear classifiers
    + What distinguishes them is the procedure for determining
      (training) the optimal weights/coefficients and the way that the
      score is interpreted.
- Examples of such algorithms are:
    + Logistic regression and Multinormial logistic regression
    + Probit regression
    + The perceptron algorithm
    + Support vector machines
    + Fisher's Linear discriminant analysis
    + Naive Bayes classifier

## Other algorithms

- Least squares support vector machines
- Quadratic classifiers
- Kernel estimation
    + k-nearest neighbor
- Boosting (meta-algorithm)
- Decision trees
    + Random forests
    + Decision stream
- Neural networks
- Learning vector quantization

# Evaluation

## Introduction

- classifier performance depends greatly on the characteristics of the
  data to be classified => no-free-lunch theorem
    + for certain types of mathematical problems, the computational cost
      of finding a solution, averaged over all problems in the class, is
      the same for any solution method.
- The measures precision and recall are popular metrics used to evaluate
  the quality of a classification system
    + recently, receiver operating characteristic (ROC) curves have been
      used to evaluate the trade-off between true- and false-positive
      rates of classification algorithms
- As a performance metric, the uncertainty coefficient has the advantage
  over simple accuracy in that it is not affected by the relative sizes
  of the different classes.
    + The uncertainty coefficient does not penalize an algorithm for
      simply rearranging the classes

## Precision and accuracy

- Precision is a description of random errors, a measure of statistical
  variability
- Accuracy has two definitions
    + more commonly, it is a description of systematic errors, a measure
      of statistical bias; as these cause a difference between a result
      and a "true" value, ISO calls this trueness.
    + alternatively, ISO defines accuracy as describing a combination of
      both types of observational error above (random and systematic),
      so high accuracy requires both high precision and high trueness.
- In simplest terms, given a set of data points from repeated
  measurements of the same quantity
    + the set can be said to be precise if the values are close to each
      other
    + while the set can be said to be accurate if their average is close
      to the true value of the quantity being measured.
    + The two concepts are independent of each other, so a particular
      set of data can be said to be either accurate, or precise, or
      both, or neither.

## Precision and Recall

### False positives and false negatives

- A false positive is an error in data reporting in which a test result
  improperly indicates presence of a condition, such as a disease (the
  result is positive), when in reality it is not present.
- A false negative is an error in which a test result improperly
  indicates no presence of a condition (the result is negative), when in
  reality it is present.
- True positive => positive, true negative => negative
    + Good data
    + false positive/negative => ERROR!!!

```
// Contingency table

              T    Predict      F
        +-------------+--------------+
      T |     TP      |      FN      |
Actual  |             |              |
        +----------------------------+
      F |     FP      |      TN      |
        +-------------+--------------+

Precision = TP / (TP + FP)
    + also known as positive predictive value
Recall = TP / (TP + FN)
    + also known as sensitivity
```

### Understanding precision and recall

- Both precision and recall are based on an understanding and measure of
  relevance
- When a search engine returns 30 pages only 20 of which were relevant
  while failing to return 40 additional relevant pages, its precision is
  20/30 = 2/3 while its recall is 20/60 = 1/3. So, in this case,
  precision is "how useful the search results are", and recall is "how
  complete the results are".
- Precision can be seen as a measure of `exactness or quality`, whereas
  recall is a measure of `completeness or quantity`.
- In simple terms, high precision means that an algorithm returned
  substantially `more relevant results` than irrelevant ones, while high
  recall means that an algorithm returned `most of the relevant
  results`.

### Examples and the relationship between precision and recall

- In an information retrieval scenario, the instances are documents and
  the task is to return a set of relevant documents given a search term;
  or equivalently, to assign each document to one of two categories,
  "relevant" and "not relevant". In this case, the "relevant" documents
  are simply those that belong to the "relevant" category. Recall is
  defined as the number of relevant documents retrieved by a search
  divided by the total number of existing relevant documents, while
  precision is defined as the number of relevant documents retrieved by
  a search divided by the total number of documents retrieved by that
  search.
    + In information retrieval, a perfect precision score of 1.0 means
      that every result retrieved by a search was relevant (but says
      nothing about whether all relevant documents were retrieved)
      whereas a perfect recall score of 1.0 means that all relevant
      documents were retrieved by the search (but says nothing about how
      many irrelevant documents were also retrieved).
- In a classification task, the precision for a class is the number of
  true positives (i.e. the number of items correctly labeled as
  belonging to the positive class) divided by the total number of
  elements labeled as belonging to the positive class (i.e. the sum of
  true positives and false positives, which are items incorrectly
  labeled as belonging to the class). Recall in this context is defined
  as the number of true positives divided by the total number of
  elements that actually belong to the positive class (i.e. the sum of
  true positives and false negatives, which are items which were not
  labeled as belonging to the positive class but should have been).
    + In a classification task, a precision score of 1.0 for a class C
      means that every item labeled as belonging to class C does indeed
      belong to class C (but says nothing about the number of items from
      class C that were not labeled correctly) whereas a recall of 1.0
      means that every item from class C was labeled as belonging to
      class C (but says nothing about how many other items were
      incorrectly also labeled as belonging to class C).
- Often, there is `an inverse relationship between precision and recall`,
  where it is possible to increase one at the cost of reducing the
  other.
    + Brain surgery provides an illustrative example of the tradeoff.
      Consider a brain surgeon tasked with removing a cancerous tumor
      from a patient’s brain. The surgeon needs to remove all of the
      tumor cells since any remaining cancer cells will regenerate the
      tumor. Conversely, the surgeon must not remove healthy brain cells
      since that would leave the patient with impaired brain function.
      The surgeon may be more liberal in the area of the brain she
      removes to ensure she has extracted all the cancer cells. This
      decision increases recall but reduces precision. On the other
      hand, the surgeon may be more conservative in the brain she
      removes to ensure she extracts only cancer cells. This decision
      increases precision but reduces recall. That is to say, greater
      recall increases the chances of removing healthy cells (negative
      outcome) and increases the chances of removing all cancer cells
      (positive outcome). Greater precision decreases the chances of
      removing healthy cells (positive outcome) but also decreases the
      chances of removing all cancer cells (negative outcome).
- Usually, precision and recall scores are not discussed in isolation.
  Instead, either values for one measure are compared for a fixed level
  at the other measure (e.g. precision at a recall level of 0.75) or
  both are combined into a single measure.
    + Examples of measures that are a combination of precision and
      recall are the F-measure (the weighted harmonic mean of precision
      and recall), or the Matthews correlation coefficient, which is a
      geometric mean of the chance-corrected variants: the regression
      coefficients Informedness (DeltaP') and Markedness (DeltaP).
- Inverse Precision and Inverse Recall are simply the Precision and
  Recall of the inverse problem where positive and negative labels are
  exchanged (for both real classes and prediction labels).
- Recall and Inverse Recall, or equivalently true positive rate and
  false positive rate, are frequently plotted against each other as ROC
  curves and provide a principled mechanism to explore operating point
  tradeoffs.

## Uncertainty coefficient

- In statistics, the uncertainty coefficient, also called proficiency,
  entropy coefficient or Theil's U, is a measure of nominal association.

# Application

- Computer vision
    + Medical imaging
    + Optical character recognition
    + Video tracking
- Drug discovery and development
    + Toxicogenomics
    + Quantitative structure-activity relationship
- Geostatistics
- Speech recognition
- Handwriting recognition
- Biometric identification
- Biological classification
- Statistical natural language processing
- Document classification
- Internet search engines
- Credit scoring
- Pattern recognition
- Micro-array classification

# References

