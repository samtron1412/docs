[TOC]

# Overview

- A subset of artificial intelligence
- often uses statistical techniques to give computers the ability to
  *learn* (i.e., progressively improve performance on a specific task)
  with data, without being explicitly programmed.
    + data-driven predictions or decisions
- The term was coined in 1959 by Arthur Samuel
    + Evolved from the study of pattern recognition and computational
      learning theory in artificial intelligence
- Machine Learning Process
    + Preprocessing
        * extract, transform, and load data to staging area
        * review data for missing data and invalid values
            - set to default values or ignore those records
        * normalizing and scaling numeric data
            - changing the range of values in a feature or attribute
        * standardize categorical values
            - ISO standard, etc.
    + Model Building
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
    + Validation
        * assess the quality of models built in step 2
        * applying models to additional test sets
        * measuring quality of models (metrics)
            - accuracy
            - precision (positive predictive value)
            - and sensitivity (recall)

# Tasks

- Supervised Learning: the computer is presented with example inputs and
  their desired outputs
    + Semi-supervised learning: the computer is given only an incomplete
      training signal: a training set with some of the target outputs
      missing
    + Active learning: the computer can only obtain training labels for
      a limited set of instances
    + Reinforcement learning: training data (in form of rewards and
      punishments) is given only as feedback to the program's actions in
      a dynamic environment, such as driving a vehicle or playing a game
      against an opponent
- Unsupervised learning: no labels are given to the learning algorithm,
  leaving it on its own to find structure in its input.
    + can be a goal in itself (discovering hidden patterns in data)
    + means towards an end (feature learning)
    + use cases
        * recommendations

# Applications

- Classification
    + inputs are divided into two or more classes (multiclass
      classification, and the learner must produce a model that assigns
      unseen inputs to one or more (multi- label classification) of
      these classes.
    + typically in a supervised manner
    + e.g. spam filtering
- Regression
    + produce a function that describes relationships between inputs and
      outputs (variable relationship)
        * prediction and forecasting
    + a supervised problem
    + the outputs are continuous rather than discrete
- Clustering
    + a set of inputs is to be divided into groups
    + unlike in classification, the groups are not known beforehand =>
      unsupervised task
        * different groups of customers
- Density estimation
    + finds the distribution of inputs in some space
- Dimensionality reduction
    + simplifies inputs by mapping them into a lower-dimensional space

# Approaches

## Decision tree learning

Something

## Association rule learning

Something

## Artificial neural networks

Something

### Deep learning

Something

## Inductive logic programming

Something

## Support vector machines (SVMs)

Something

## Clustering

Something

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

## Genetic algorithms

Something

## Rule-based machine learning

Something

### Learning classifier systems

Something

# References

