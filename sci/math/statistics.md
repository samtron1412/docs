[TOC]

# Overview

- Statistics is a branch of mathematics dealing with the collection,
  analysis, interpretation, presentation, and organization of data.
- Researchers use statistics to analyze and understand the results of
  research studies.
- Two broad categories
    + Descriptive statistics: to describe data (to classify and
      summarize information expressed in numerical form)
    + Inferential statistics: to make generalizations about a population
      by studying results based on a sample drawn from the population

# Applications of Statistics

Three main purpose of statistics in scientific inquiry

1. To describe
2. To relate
3. To compare

## To Describe

### Frequency Distribution

The first step in describing a distribution of values is to develop a
frequency distribution is a graph of frequencies of values
- histogram: bar graph
- frequency polygon: straight lines

### Central Tendency

The second step in describing a distribution of values is to compute the
central tendency
- central tendency is an indicator of the average score in a
  distribution of values
- Three different statistical measures of central tendency:
    + mode (most frequent value)
    + median (middle score)
    + mean (arithmetic average)

### Measures of Variability

The final step in describing a distribution of values is to compute the
variability of the values
- Variability is the spread of values throughout the distribution of
  values
- One measure of variability is the *range* of values, the difference
  between the highest and lowest values in the distribution.
- Another measure of variability is the *standard deviation*: the
  average difference between each individual value and the mean of all
  scores in the data set.
    + A large standard deviation -> considerable variability (spread) of
      values around the mean
    + A small standard deviation -> little variability
    + Calculate standard deviation
        * calculate deviation (difference) from mean for each value (D)
        * square the deviations and sum them up (sum(Di^2))
        * divide the sum by the number of values (sum(Di^2)/n)
        * take square root of the value -> standard deviation
        * SD = sqrt(sum(Di^2)/n)

### The normal distribution

The values distribute in the middle of the distribution, with fewer
values in the extreme categories.
- a bell-shaped curve
- the mean, mode, median have the same value
- we can determine the percentages of cases that fall within each
  segment of the distribution.
- the properties of the normal distribution can also be used to describe
  the distance between a value and the mean -> applying in inferential
  statistics

## To Relate

A second application of statistics involves determining the relationship
between two variables.

### The Scatter-plot: Plotting the data

Our first step would be to enter these data in a scatterplot, a type of
graph that represents the scatter of values obtained by plotting each
individual's value on two variables.
- Positive Correlation: If the pattern of points on the graph starts in
  the lower left corner and ends in the upper right corner of the
  scatterplot -> higher values on one variable are associated with
  higher values on the other variable.
- Negative Correlation: downward trend -> higher values on one variable
  are associated with lower values on the other variable.
- Zero Correlation: no relationship

### The Correlation Coefficient: Calculating the Relationship Between Two Variables

The correlation coefficient (r)
- positive correlation: 0 <= r <= +1
- negative correlation: -1 <= r <= 0

| Size of Correlation | Interpretation                  |
| -                   | -                               |
| .90 - 1.00          | Very high positive  correlation |
| .70 - .90           | High positive correlation       |
| .50 - .70           | Moderate                        |
| .30 - .50           | Low                             |
| .00 - .30           | Little if any correlation       |

### Using One Variable to Predict Another

An important use of correlational statistics is prediction
- If two variables are correlated, we can predict values on one variable
  based up on values of the other variable.
- The process of prediction
    + Developing a mathematical equation that incorporates the paired
      sets of scores on the two variables obtained in the study ->
      regression lines
    + The higher correlation,, the better the prediction

## To Compare

A third application of statistics involves comparing two or more groups.

## Beyond Description: Using Inferential Statistics

Descriptive statistics allow us to summarize data, but the meaning of
these statistical measures cannot be fully understood through
descriptive statistics alone.
- Statistical significant: indicates that the results obtained from a
  study are unlikely to have been due to chance  or to the random
  fluctuations that would be expected to occur among values in the
  general population.

### Stating the Null Hypothesis

The first step in using inferential statistics is to state a *null
hypothesis* for the study in question.

- A null hypothesis is a prediction that a given finding has no value or
  significance.
- There is no difference between the control groups and the experimental
  groups.

### Testing the Null Hypothesis

The result is judged to be significant when its likelihood of arising
from chance is less then 5 percent.

- if the probability that an outcome would occur by chance alone is less
  than 5 percent, they would say that the finding is statistically
  significant

# Techniques

## Gaussian Discriminant Analysis

### Linear Discriminant Analysis (LDA)

- To classify data into categories
- Compute the boundary such that projected data on the boundary is
  separated into groups
    + maximize the distance between means: (m1 - m2)^2
    + miminmize the scatter of data (std dev 1, 2)


# Common Functions

- Logit function: https://en.wikipedia.org/wiki/Logit
    + Log-odds: `ln(odds) = ln[p/(1-p)]`
    + https://www.quora.com/Why-should-we-use-log-of-odds-in-logistics-regression-and-not-the-same-in-linear-regression
    + https://towardsdatascience.com/https-towardsdatascience-com-what-and-why-of-log-odds-64ba988bf704#:~:text=You%20can%20see%20from%20the,non%2Dfraud%2C%20type%20scenarios.
    + https://www.youtube.com/watch?v=ARfXDSkQf1Y

# Glossary

## Contingency table

- In statistics, a contingency table (also known as a cross tabulation
  or crosstab) is a type of table in a matrix format that displays the
  (multivariate) frequency distribution of the variables.

## Frequency distribution

- A frequency distribution is a tabular form of statistics. Each entry
  in the table contains the frequency of count of the occurrences of
  values within a particular group or interval, and in this way, the
  table summarizes the distribution of values in the sample.

# References

[wiki]: https://en.wikipedia.org/wiki/Statistics
[degree-of-freedom]: https://en.wikipedia.org/wiki/Degrees_of_freedom_(statistics)
[cross-validation]: https://en.wikipedia.org/wiki/Cross-validation_(statistics)
