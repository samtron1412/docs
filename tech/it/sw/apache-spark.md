[TOC]

# Overview

- An open-source cluster-computing framework
    + it supports not only MapReduce but also SQL queries, streaming
      data, machine learning, and graph algorithms
- Apache Spark has as its architectural foundation the resilient
  distributed dataset (RDD), a read-only multiset of data items
  distributed over a cluster of machines, that is maintained in a
  fault-tolerant way.
    + Spark 1.x, the RDD was the primary API
    + Spark 2.x, the Dataset API is encouraged
- Spark and its RDDs were developed in 2012 in response to limitations
  in the MapReduce cluster computing paradigm, which forces a particular
  linear dataflow structure on distributed programs.
- Spark requires a cluster manager and a distributed storage system.
    + cluster management
        * standalone (native Spark cluster)
        * Hadoop YARN
        * Apache Mesos
    + distributed storage, Spark can interface with a wide variety
        * HDFS
        * MapR-FS
        * Cassandra
        * OpenStack
        * Swift
        * Amazon S3, Kudu
- Modes of running
    + Local
    + Standalone
    + cluster management frameworks
        * YARN
        * Mesos

# Installation

- Download the Apache Spark
- Extracting the tar file
- Moving Spark to your location
- Setting up the environment variables
    + add bin to PATH
- Verifying the Spark installation
    + spark-shell
    + web-ui: http://localhost:4040

# Spark Components

```
++++++++++++++++++++++++++++++++++++++++++++++++
| Spark SQL | Spark Streaming | MLlib | GraphX |
++++++++++++++++++++++++++++++++++++++++++++++++
|            Apache Spark Core                 |
++++++++++++++++++++++++++++++++++++++++++++++++
```

+ Spark Core
    * provides distributed task dispatching, scheduling, and basic
      I/O functionalities, exposed through an API (Java, Python,
      Scala, and R) centered on the RDD abstraction.
+ Spark SQL
    * a component on top of Spark Core that introduced a data
      abstraction called DataFrames, which provides support for
      structured and semi-structured data.
    * Spark SQL provides a domain-specific language (DSL) to
      manipulate DataFrames in Scala, Java, or Python.
    * provides SQL language support, with command-line interfaces
      and ODBC/JDBC server
+ Spark Streaming
    * Spark Streaming uses Spark Core's fast scheduling capability
      to perform streaming analytics.
    * It ingests data in mini-batches and performs RDD
      transformations on those mini-batches of data.
    * built-in to consume from Kafka, Flume, Twitter, ZeroMQ,
      Kinesis, and TCP/IP sockets
+ MLlib
    * a distributed machine learning framework on top of Spark Core
    * common machine learning and statistical algorithms
        - summary statistics, correlations, stratified sampling,
          hypothesis testing, random data generation
        - classification and regression: support vector machines,
          logistic
        - collaborative filtering techniques including alternating
          least squares (ALS)
        - cluster analysis methods including k-means, and latent
          Dirichlet allocation (LDA)
        - dimensionality reduction techniques such as singular value
          decomposition (SVD), and principal component analysis
          (PCA)
        - feature extraction and transformation functions
        - optimization algorithms such as stochastic gradient
          descent, limited-memory BFGS
+ GraphX
    * distributed graph processing framework on top of Apache Spark

# Resilient Distributed Dataset (RDD)

## Why?

- Data Sharing is Slow in MapReduce due to *replication*,
  *serialization*, and *disk IO*.
- RDDs support in-memory processing computation
    + it stores the state of memory as an object across the jobs and the
      object is sharable between those jobs.

## Introduction

- a fundamental data structure of Spark
    + an immutable distributed collection of objects
    + each dataset in RDD is divided into logical partitions, which may
      be computed on different nodes of the cluster
    + RDDs can contain any type of Python, Java, Scala objects,
      including user-defined classes
    + RDDs can be created
        * through deterministic operations on either data on stable
          storage
        * or other RDDs
    + There are two ways to create RDDs
        * parallelizing an existing collection in your driver program
        * referencing a dataset in an external storage system, such as
          shared file system, HDFS, HBase, or any data source offering a
          Hadoop Input Format

## Operations

+ Two types of operations
    * transformations
    * actions

### Transformations

- to change the RDD in some way, such as filtering out some data
- RDDs are immutable => the end of result of all transformations result
  in the creation of a new RDD
- RDDs perform transformations lazily
- transformations return pointer to new RDD and allows you to crate
  dependencies between RDDs.
    + each RDD in dependency chain (String of Dependency) has a function
      for calculating its data and has a pointer (dependency) to its
      parent RDD

| S.No | Transformations and Meaning                                                                                                                                                        |
| 1    | map(func): returns a new distributed dataset, formed by passing each element of the source through a function func                                                                 |
| 2    | filter(func): returns a new dataset formed by selecting those elements of the source on which func returns true.                                                                   |
| 3    | flatMap(func): similar to map, but each input item cna be mapped to 0 or more output items (so func should return a Seq rather than a single item)                                 |
| 4    | mapPartitions(func): similar to map, but runs separately on each partition (block) of the RDD, so func ust be of type Iterator<T> => Iterator<U> when running on an RDD of type T. |
| 5    | ...                                                                                                                                                                                |



### Actions

- use the data contained in the RDDs, and as such when an action is
  called on an RDD, this is when the transformations are performed.

| S.No | Action and Meaning                                                                                                                                                                                                           |
| -    | -                                                                                                                                                                                                                            |
| 1    | reduce(func): Aggreagate the elements of the datset using a function func (which takes two arguments and returns one). The function should be commutative and assoociative so that it can be computed correclty in parallel. |
| 2    | collect(): returns all the elements of the dataset as an array at the driver program. This is usually useful after a filter or other operation that returns a sufficiently small subset of the data.                         |
| 3    | count(): Returns the number of elements in the dataset.                                                                                                                                                                      |
| 4    | first(): returns the first element of the dataset (similar to take(1))                                                                                                                                                       |
| 5    | take(n): returns an arrya with the first n elements of the dataset                                                                                                                                                           |
| 6    | takeSample(withReplacement, num, [seed]): returns an array with a random sample of num elements of the dataset, with or without replacement, optionally pre-specifying a random number generator seed.                       |
| 7    | ...                                                                                                                                                                                                                          |


# Quick Start

- https://spark.apache.org/docs/latest/quick-start.html
- spark-shell
    + web-ui: http://localhost:4040
    + interactive shell, scripting
- self-contained applications (jar)
    + sbt for Scala, Maven for Java
- examples
    + https://github.com/apache/spark/tree/master/examples/src/main/scala/org/apache/spark/examples

```
// build.sbt

name := "Simple Project"

version := "1.0"

scalaVersion := "2.11.8"

libraryDependencies += "org.apache.spark" %% "spark-sql" % "2.3.1"
```

```
# Your directory layout should look like this
$ find .
.
./build.sbt
./src
./src/main
./src/main/scala
./src/main/scala/SimpleApp.scala

# Package a jar containing your application
$ sbt package
...
[info] Packaging {..}/{..}/target/scala-2.11/simple-project_2.11-1.0.jar

# Use spark-submit to run your application
$ YOUR_SPARK_HOME/bin/spark-submit \
  --class "SimpleApp" \
  --master local[4] \
  target/scala-2.11/simple-project_2.11-1.0.jar
...
Lines with a: 46, Lines with b: 23
```

# References

[streaming]: https://www.linkedin.com/pulse/spark-streaming-vs-flink-storm-kafka-streams-samza-choose-prakash
[sql]: https://www.dezyre.com/article/spark-sql-vs-apache-drill-war-of-the-sql-on-hadoop-tools/234
