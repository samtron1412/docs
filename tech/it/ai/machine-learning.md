[TOC]

# Overview

- https://en.wikipedia.org/wiki/Machine_learning
- A subset of artificial intelligence
- often uses statistical techniques to give computers the ability to
  *learn* (i.e., progressively improve performance on a specific task)
  with data, without being explicitly programmed.
    + data-driven predictions or decisions
- The term was coined in 1959 by Arthur Samuel
    + Evolved from the study of pattern recognition and computational
      learning theory in artificial intelligence

# State of the Art (SOTA)

- https://paperswithcode.com/

# Courses

- https://www.coursera.org/learn/machine-learning
- https://eecs189.org/
    + https://www.bilibili.com/video/BV1Gr4y1s7nF
    + https://www.youtube.com/playlist?list=PLCuQm2FL98HTlRmlwMk2AuFEM9n1c06HE
    + https://www.youtube.com/watch?v=slGymxkELYE&list=PLOOm2AoWIPEyZazQVnIcaK2KnezpGZV-X
- https://cs229.stanford.edu/
    + https://www.bilibili.com/video/BV1JE411w7Ub/

# Tasks

- **Supervised Learning**: the computer is presented with example inputs
  and their desired outputs
    + **Semi-supervised learning**: the computer is given only an
      incomplete training signal: a training set with some of the target
      outputs missing
    + **Active learning**: the computer can only obtain training labels
      for a limited set of instances
    + **Reinforcement learning**: training data (in form of rewards and
      punishments) is given only as feedback to the program's actions in
      a dynamic environment, such as driving a vehicle or playing a game
      against an opponent
- **Unsupervised learning**: no labels are given to the learning
  algorithm, leaving it on its own to find structure in its input.
    + can be a goal in itself (discovering hidden patterns in data)
    + means towards an end (feature learning)
    + use cases
        * recommendations

# Applications

- **Classification**
    + inputs are divided into two or more classes (multiclass
      classification, and the learner must produce a model that assigns
      unseen inputs to one or more (multi-label classification) of
      these classes.
    + typically in a supervised manner
    + e.g. spam filtering
- **Regression**
    + produce a function that describes relationships between inputs and
      outputs (variable relationship)
        * prediction and forecasting
    + a supervised problem
    + the outputs are continuous rather than discrete
- **Clustering**
    + a set of inputs is to be divided into groups
    + unlike in classification, the groups are not known beforehand =>
      unsupervised task
        * different groups of customers
    + explores the datasets
- **Density estimation**
    + finds the distribution of inputs in some space
    + Gaussian Discriminant Analysis (GDA): Quadratic Discriminant
      Analysis (QDA), Linear Discriminant Analysis (LDA)
- **Dimensionality reduction**
    + simplifies inputs by mapping them into a lower-dimensional space
    + Principal Component Analysis (PCA)

# Feature

## Introduction

- A feature is an individual measurable property or characteristic of a
  phenomenon being observed.
- Choosing informative, discriminating and independent features is a
  crucial step for effective algorithms in pattern recognition,
  classification and regression.
- Features are usually numeric, but structural features such as strings,
  and graphs are used in syntactic pattern recognition.
- The concept of feature is related to that of independent variable used
  in statistical techniques such as linear regression.

## Examples

- In character recognition, features may include histograms counting the
  number of black pixels along horizontal and vertical directions,
  number of internal holes, stroke detection and many others.
- In speech recognition, features fro recognizing phonemes can include
  noise ratios, length of sounds, relative power, filter matches and
  many others.
- In spam detection algorithms, features may include the presence or
  absence of certain email headers, the email structure, the language,
  the frequency of specific terms, the grammatical correctness of the
  text.
- In computer vision, there are a large number of possible features,
  such as edges and objects.

## Classification

- A set of numeric features can be conveniently described by a feature
  vector.
- Algorithms for classification from a feature vector include nearest
  neighbor classification, neural networks, and statistical techniques
  such as Bayesian approaches.

## Feature vector

- A feature vector is an n-dimensional vector of numerical features that
  represent some object.
- Many algorithms in machine learning require a numerical representation
  of objects, since such representations facilitate processing and
  statistical analysis.
- When representing images, the feature values might correspond to the
  pixels of an image, while when representing texts the features might
  be the frequencies of occurrence of textual terms.
- Feature vectors are often combined with weights using a dot product in
  order to construct a linear predictor function that is used to
  determine a score for making a prediction.
- The vector space associated with these vectors is often called the
  feature space.
    + In order to reduce the dimensions of the feature space, a number
      of dimension reduction techniques can be employed.
- Higher-level features are obtained from already available features and
  added to the feature vector.
    + For example, for the study of diseases the feature 'Age' is useful
      and is defined as Age='Year of death' minus 'Year of birth'.
    + This process is referred to as feature construction.

## Selection and extraction

- The initial set of raw features can be redundant and too large to be
  managed.
- Therefore, a preliminary step in many applications consist of
  selecting a subset of features, or constructing a new and reduced set
  of features to facilitate learning, and to improve generalization and
  interpretability.
- Extracting or selecting features require automated techniques with the
  intuition and knowledge of the domain expert.
    + Automating this process is feature learning, where a machine not
      only uses features for learning, but learn the features itself.

# Approaches

## Decision tree learning

Something

## Association rule learning

Something

## Artificial neural networks

It is inspired by the biological neural networks in animal brains.
- Multiple layers of units/nodes/artificial neurons: each neuron
  contains a number/value
- The connections between units are weights that will be multiplied with
  the value in that neurons.

### Calculus

- Derivatives of common activation functions
    + https://theclevermachine.wordpress.com/2014/09/08/derivation-derivatives-for-common-neural-network-activation-functions/

### Convolutional Neural Networks (CNNs)

CNN is a neural network with two characteristics:
1. Shared-weights architecture
2. Translation invariance: using convolution operation

It is inspired by biological processes, the animal visual cortex.
- It is usually used in computer vision.

### Recurrent Neural Networks (RNNs)

RNN is a neural network that can model the temporal dynamic behaviors.
- Nodes in a layer can have connections back to the nodes in the same
  layer (mixed forward connections and feedback connections)
- It is usually used in speech/handwritten recognition.

### Deep learning

Many layers of units (artificial neurons) in a neural network between
input and output layers.
- e.g., CNNs, RNNs

## Inductive logic programming

Something

## Support Vector Machines (SVMs)

Something

## Clustering

- Algorithms
    + K-means: small and mix-sized data sets
    + Hierarchical clustering with Bisecting K-means: large data sets

## Bayesian networks

Something

## Reinforcement learning

Something

## Representation learning

Something

## Similarity and metric learning

Something

## Sparse dictionary learning

Something

## Genetic Algorithms

Something

## Rule-based Machine Learning

Something

### Learning Classifier Systems

Something


# Machine Learning Process

## Preprocessing

### Introduction

* extract, transform, and load data to staging area
* review data for missing data and invalid values
    - set to default values or ignore those records
* normalizing and scaling numeric data
    - changing the range of values in a feature or attribute
* standardize categorical values
    - ISO standard, etc.


### Feature scaling

- https://en.wikipedia.org/wiki/Feature_scaling
- Normalization, Standardization

## Model Building

### Introduction

* selecting algorithms
* apply machine learning algorithms to training data
    - fitting a model to the data
* some algorithms require tuning hyperparameters
    - how many levels to have in a decision tree
    - need to experiment to find optimal hyperparameters
    - when we set a parameter to the machine learning algorithm,
      we call those parameters hyperparameters.
    - when the machine learning algorithm learns the value of
      the parameter from training data, then we call those
      simply parameters

## Validation

### Introduction

* assess the quality of models built in step 2
* applying models to additional test sets
* measuring quality of models (metrics)
    - accuracy
    - precision (positive predictive value)
    - and sensitivity (recall)
* K-fold-cross-validation

# Regularization

## Introduction

- https://en.wikipedia.org/wiki/Regularization_(mathematics)
- Regularization is a process of introducing additional information in
  order to solve an ill-posed problem or to prevent over-fitting.
    + Add a brake to the fitting model

# Convergence tolerance

- http://www.nbertagnolli.com/jekyll/update/2015/10/03/ConvTol.html
- There are three different methods of declaring a convergence:
    + *absolute tolerance*, relative tolerance and running for a
      specified number of iterations. In the absolute tolerance mode
      algorithm stops when an absolute difference in any of the
      variables is lower than the threshold.
    + *relative tolerance* In this method I compute the difference
      between the new approximation and the old one for each of the
      variables and divide it by the previous(old) value of the variable
      (in case it is not equal to 0).
    + *number of iterations* Here we let the algorithm run for the
      specified number of steps no matter what absolute or relative
      error was obtained before that and return the approximation on the
      last step as the result of the computation.

# Datasets for research and training models

## Classification

- Two classes
    + https://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html

# References

[kkt-conditions]: https://en.wikipedia.org/wiki/Karush%E2%80%93Kuhn%E2%80%93Tucker_conditions
[convex-set]: https://en.wikipedia.org/wiki/Convex_set
[vc-dimension]: https://en.wikipedia.org/wiki/VC_dimension
[vc-theory]: https://en.wikipedia.org/wiki/Vapnik%E2%80%93Chervonenkis_theory
[control-theory]: https://www.reddit.com/r/MachineLearning/comments/at5iau/d_does_learning_control_theory_helps_to/
[gradient-descent]: https://en.wikipedia.org/wiki/Gradient_descent
