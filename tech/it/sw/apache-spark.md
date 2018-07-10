[TOC]

# Overview

## History

- An open-source cluster-computing framework
    + it supports not only MapReduce but also SQL queries, streaming
      data, machine learning, and graph algorithms
- 2003: Nutch project: open distributed platform
- 2004: Google published a white page on MapReduce
- 2006: Yahoo hires Nutch developers, and releases Hadoop
- 2008: Facebook launched Hive
    + MapReduce: Java-based, batch-oriented, and slow
    + Hive: SQL abstraction on top of MapReduce
- 2009: Spark was born at AMPLab at UC Berkeley
    + 2010: open source Spark
    + 2014: Spark becomes a top-level Apache project

## Key Features

- Apache Spark has as its architectural foundation the resilient
  distributed dataset (RDD), a read-only multiset of data items
  distributed over a cluster of machines, that is maintained in a
  fault-tolerant way.
    + Spark 1.x, the RDD was the primary API
    + Spark 2.x, the Dataset API is encouraged
- Spark and its RDDs were developed in 2012 in response to limitations
  in the MapReduce cluster computing paradigm, which forces a particular
  linear dataflow structure on distributed programs.

## Cluster Managers and Distributed Storage Systems

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

## Use Cases

- Streaming ETL: Data Integration
    + Moving data from one location to another and standardizing it so
      it's easy to use by analysts and data scientist
    + Uber converts mobile events into structured data and responds to
      aggregate event data more quickly
- Data enrichment
    + Pinterest converts user interaction around pins and increased
      customer engagement via faster feedback
- Trigger event detection
    + Conviva manages video stream quality and prevents customer churn
      by responding to issues more rapidly

# Hardware Provisioning

- https://spark.apache.org/docs/latest/hardware-provisioning.html

## Storage Systems

- run Spark on the same nodes as HDFS
- set up a Spark standalone mode cluster on the same nodes, and
  configure Spark and Hadoop's memory and CPU usage to avoid
  interference
    + Hadoop
        * per-task memory: `mapred.child.java.opts`
        * number of tasks: `mapreduce.tasktracker.map.tasks.maximum` and
          `mapreduce.tasktracker.reduce.tasks.maximum`
- for low-latency data stores like HBase, it may be preferable to run
  computing jobs on different nodes than the storage system to avoid
  interference

## Local Disks

- 4-8 disks per node
- mount the disks with the noatime option
    + http://www.centos.org/docs/5/html/Global_File_System/s2-manage-mountnoatime.html
- configure `spark.local.dir` variable to be a comma-separated list of
  the local disks

## Memory

- allocating at most 75% of the memory for Spark; leave the rest for the
  operating system and buffer cache
- how much memory you will need depend on your application
- Java VM does not always behave well with more than 200 GB of RAM
    + you can run multiple worker JVMs per node
    + `SPARK_WORKER_INSTANCES` in `conf/spark-env.sh`
    + `SPARK_WORKER_CORES` the number of cores per worker

## Network

- distributed reduce
    + group-bys, reduce-bys, SQL joins
- using a 10 Gigabit or higher network
- web UI: how much data Spark shuffles across the network
    + http://<driver-node>:4040

## CPU Cores

- 8-16 cores per machine

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
    * provides distributed task distribution, scheduling, and basic I/O
      functionalities, exposed through an API (Java, Python, Scala, and
      R) centered on the RDD abstraction.
+ Spark SQL
    * a component on top of Spark Core that introduced a data
      abstraction called DataFrames, which provides support for
      structured and semi-structured data.
    * Spark SQL provides a domain-specific language (DSL) to manipulate
      DataFrames in Scala, Java, or Python.
    * provides SQL language support, with command-line interfaces and
      ODBC/JDBC server
+ Spark Streaming
    * Spark Streaming uses Spark Core's fast scheduling capability to
      perform streaming analytics.
    * It ingests data in micro-batches and performs RDD transformations
      on those micro-batches of data.
    * built-in to consume from Kafka, Flume, Twitter, ZeroMQ, Kinesis,
      and TCP/IP sockets
    * Lambda architecture: both batch and stream-processing methods
        - batch: comprehensive and accurate views
        - real-time stream processing
+ MLlib
    * a distributed machine learning framework on top of Spark Core
    * common machine learning and statistical algorithms
        - summary statistics, correlations, stratified sampling,
          hypothesis testing, random data generation
        - classification and regression: support vector machines,
          logistic
        - collaborative filtering techniques including alternating least
          squares (ALS)
        - cluster analysis methods including k-means, and latent
          Dirichlet allocation (LDA)
        - dimensionality reduction techniques such as singular value
          decomposition (SVD), and principal component analysis (PCA)
        - feature extraction and transformation functions
        - optimization algorithms such as stochastic gradient descent,
          limited-memory BFGS
+ GraphX
    * distributed graph processing framework on top of Apache Spark
    * in-memory version of Apache Giraph
    * based on DataFrames -> it's not a true graph database
      implementation

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


# Spark SQL, Datasets, and DataFrames

- https://spark.apache.org/docs/latest/sql-programming-guide.html

# Spark Streaming

- https://spark.apache.org/docs/latest/streaming-programming-guide.html
- Streaming processing (not an Streaming ingest service)
    + Micro-batching
- Streaming ingest services
    + Apache Kafka
    + Amazon Kinesis
    + Google Cloud Pub/Sub
    + Azure Service Bus
- MLeap Spark
    + train an ML pipeline with Spark then export it to Bundle.ML
    + dynamically deploy the model into production (easier)

# MLlib

## Introduction

- https://spark.apache.org/docs/latest/ml-guide.html
- Components
    + Algorithms: classification, regression, clustering, topic
      modeling, etc.
    + Workflows: feature transformations, pipelines, evaluations, and
      hyperparameter tuning
    + Utilities: distributed math libraries and statistics functions

## Two types of pre-processing

### Numeric data

#### Introduction

+ normalize
    * maps data values from their original range to the range of 0 to 1
+ standardize
    * maps data values from their original range to -1 to 1
    * mean value of 0
    * normally distributed with standard deviation of 1
    * this transforms the data into the bell curve shape formation
    * used when attributes have different scales and ML algorithms
      assume a normal distribution. Some algorithms work better when we
      have unit variance and zero mean across all of the features.
+ Partitioning (Bucketizing)
    * Map data values from continuous values to buckets, like histograms
    * Deciles and percentiles are examples of buckets
    * Useful when you want to work with groups of values instead of a
      continuous range of values

#### Normalizing

```bash
>>> from pyspark.ml.feature import MinMaxScaler
>>> from pyspark.ml.linalg import Vectors
>>> features_df = spark.createDataFrame([
... (1, Vectors.dense([10.0, 10000.0, 1.0]),),
... (2, Vectors.dense([20.0, 30000.0, 2.0]),),
... (3, Vectors.dense([30.0, 40000.0, 3.0]),)
... ],["id","features"])
>>> features_df.take(1)
[Row(id=1, features=DenseVector([10.0, 10000.0, 1.0]))]
>>> feature_scaler =
>>> MinMaxScaler(inputCol="features",outputCol="sfeatures")
>>> smodel = feature_scaler.fit(features_df)
>>> sfeatures_df = smodel.transform(features_df)
>>> sfeatures_df.take(1)
[Row(id=1, features=DenseVector([10.0, 10000.0, 1.0]),
sfeatures=DenseVector([0.0, 0.0, 0.0]))]
>>> sfeatures_df.select("features","sfeatures").show()
+------------------+--------------------+
|          features|           sfeatures|
+------------------+--------------------+
|[10.0,10000.0,1.0]|       [0.0,0.0,0.0]|
|[20.0,30000.0,2.0]|[0.5,0.6666666666...|
|[30.0,40000.0,3.0]|       [1.0,1.0,1.0]|
+------------------+--------------------+
```

#### Standardizing

```bash
>>> from pyspark.ml.feature import StandardScaler
>>> from pyspark.ml.linalg import Vectors
>>> features_df = spark.createDataFrame([
... (1, Vectors.dense([10.0, 10000.0, 1.0]),),
... (2, Vectors.dense([20.0, 30000.0, 2.0]),),
... (3, Vectors.dense([30.0, 40000.0, 3.0]),)
... ],["id","features"])
>>> features_df.take(1)
[Row(id=1, features=DenseVector([10.0, 10000.0, 1.0]))]
>>> feature_stand_scaler =
>>> StandardScaler(inputCol="features",outputCol="sfeatures",withStd=True,
>>> withMean=True)
>>> stand_smodel = feature_stand_scaler.fit(features_df)
>>> stand_sfeatures_df = stand_smodel.transform(features_df)
>>> stand_sfeatures_df.take(1)
[Row(id=1, features=DenseVector([10.0, 10000.0, 1.0]),
sfeatures=DenseVector([-1.0, -1.0911, -1.0]))]
>>> stand_sfeatures_df.show()
+---+------------------+--------------------+
| id|          features|           sfeatures|
+---+------------------+--------------------+
|  1|[10.0,10000.0,1.0]|[-1.0,-1.09108945...|
|  2|[20.0,30000.0,2.0]|[0.0,0.2182178902...|
|  3|[30.0,40000.0,3.0]|[1.0,0.8728715609...|
+---+------------------+--------------------+
```

#### Bucketizing

```bash
>>> from pyspark.ml.feature import Bucketizer
>>> splits = [-float("inf"), -10.0, 0.0, 10.0, float("inf")]
>>> b_data = [(-800.0,),(-10.5,),(-1.7,),(0.0,),(8.2,),(90.1,)]
>>> b_df = spark.createDataFrame(b_data, ["features"])
>>> b_df.show()
+--------+
|features|
+--------+
|  -800.0|
|   -10.5|
|    -1.7|
|     0.0|
|     8.2|
|    90.1|
+--------+

>>> bucketizer = Bucketizer(splits=splits, inputCol="features",
>>> outputCol="bfeatures")
>>> bucketed_df = bucketizer.transform(b_df)
>>> bucketed_df.show()
+--------+---------+
|features|bfeatures|
+--------+---------+
|  -800.0|      0.0|
|   -10.5|      0.0|
|    -1.7|      1.0|
|     0.0|      2.0|
|     8.2|      2.0|
|    90.1|      3.0|
+--------+---------+
```

### Text data

#### Introduction

- Tokenizing
    + map text from a single string to a set of tokens or words
- Term Frequency Inverse Document Frequency - TF-IDF transformation
    + map text from a single, typically long string, to a vector
      indicating the frequency of each word in a text relative to a
      group of texts
    + widely used in text classification
    + infrequently used words are more useful for distinguishing
      categories of text

#### Tokenizing

```bash
>>> from pyspark.ml.feature import Tokenizer
>>> sentences_df = spark.createDataFrame([
... (1, "This is an introduction to Spark MLlib"),
... (2, "MLlib includes libraries for classification and regression"),
... (3, "It also contains supporting tools for pipelines")],
... ["id","sentence"])
>>> sentences_df.show()
+---+--------------------+
| id|            sentence|
+---+--------------------+
|  1|This is an introd...|
|  2|MLlib includes li...|
|  3|It also contains ...|
+---+--------------------+
>>> sent_token = Tokenizer(inputCol="sentence", outputCol="words")
>>> sent_tokenized_df = sent_token.transform(sentences_df)
>>> sent_tokenized_df.show()
+---+--------------------+--------------------+
| id|            sentence|               words|
+---+--------------------+--------------------+
|  1|This is an introd...|[this, is, an, in...|
|  2|MLlib includes li...|[mllib, includes,...|
|  3|It also contains ...|[it, also, contai...|
+---+--------------------+--------------------+
```

#### TF-IDF (Text Frequency Inverse Document Frequency)

- text => tokenize into words => count the number of times of a
  particular word appears.

```bash
>>> from pyspark.ml.feature import HashingTF, IDF
>>> sentences_df
DataFrame[id: bigint, sentence: string]
>>> sentences_df.take(1)
[Row(id=1, sentence='This is an introduction to Spark MLlib')]
>>> sent_tokenized_df.take(1)
[Row(id=1, sentence='This is an introduction to Spark MLlib',
words=['this', 'is', 'an', 'introduction', 'to', 'spark', 'mllib'])]
>>> hashingTF =
>>> HashingTF(inputCol="words",outputCol="rawFeatures",numFeatures=20)
>>> sent_hfTF_df = hashingTF.transform(sent_tokenized_df)
>>> sent_hfTF_df.take(1)
[Row(id=1, sentence='This is an introduction to Spark MLlib',
words=['this', 'is', 'an', 'introduction', 'to', 'spark', 'mllib'],
rawFeatures=SparseVector(20, {1: 2.0, 5: 1.0, 6: 1.0, 8: 1.0, 12: 1.0,
13: 1.0}))]
>>> idf = IDF(inputCol="rawFeatures",outputCol="idf_features")
>>> idfModel = idf.fit(sent_hfTF_df)
>>> tfidf_df = idfModel.transform(sent_hfTF_df)
>>> tfidf_df.take(1)
[Row(id=1, sentence='This is an introduction to Spark MLlib',
words=['this', 'is', 'an', 'introduction', 'to', 'spark', 'mllib'],
rawFeatures=SparseVector(20, {1: 2.0, 5: 1.0, 6: 1.0, 8: 1.0, 12: 1.0,
13: 1.0}), idf_features=SparseVector(20, {1: 0.5754, 5: 0.6931, 6:
0.2877, 8: 0.2877, 12: 0.0, 13: 0.2877}))]
```

## Python

- VectorAssembler
- populate the cache by an action (e.g. count())
- Create a linear regression model
    + `lrModel = LinearRegression().setLabelCol("count").setFeaturesCol("features").setElasticNetParam(0.5)`
- Fitting
    + `lrFitted = lrModel.fit(training)`
- Prediction: add a new "prediction" column to the data
    + `holdout = lrFitted.transform(test)`
- RegressionMetrics model
- pipeline models (many models in a pipeline)
    + RandomForestRegressor
        * hyperparameters
        * ParamGridBuilder to search the "hyperparameter space"
    + using `Pipeline` to feed the algorithm into a `CrossValidator` to
      help prevent "overfitting"
        * CrossValidator uses `RegressionEvaluator` to test the model
          results against a metric (default is RMSE)

## Clustering

### K-means

```bash
>>> from pyspark.ml.linalg import Vectors
>>> from pyspark.ml.feature import VectorAssembler
>>> from pyspark.ml.clustering import KMeans
>>> cluster_df =
>>> spark.read.csv("/home/glider/doc/schools/lynda/Ex_Files_Spark_ML_AI/Exercise
>>> Files/Ch03/03_02/clustering_dataset.csv",header=True,inferSchema=True)
>>> vectorAssembler =
>>> vectorAssembler =
>>> VectorAssembler(inputCols=["col1","col2","col3"],outputCol="f
eatures")
>>> vcluster_df = vectorAssembler.transform(cluster_df)
>>> kmeans = KMeans().setK(3)
>>> kmeans = kmeans.setSeed(1)
>>> kmodel = kmeans.fit(vcluster_df)
>>> centers = kmodel.clusterCenters()
```

### Hierarchical clustering (Bisecting K-means)



## Advanced ML on Spark

- Tensorflow: Google and community
- MXNet: AWS and community

# GraphX

- https://spark.apache.org/docs/latest/graphx-programming-guide.html
- Graph parallel
    + Graph database

# SparkR

Something

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

## Classification

- Algorithms
    + Naive Bayes
    + Decision trees
    + Multilayer perceptron (a type of neural network)

### Naive Bayes

#### Preprocessing the data

- Read the data from files
- Normalize, standardize, or pre-processing the data
    + Change the columns' name
    + Create vectors
    + String => numerical values

```bash
>>> from pyspark.sql.functions import *
>>> from pyspark.ml.feature import VectorAssembler
>>> from pyspark.ml.feature import StringIndexer
>>> iris_df = iris_df.select(col("_c0").alias("sepal_length"),
... col("_c1").alias("sepal_width"),
... col("_c2").alias("petal_length"),
... col("_c3").alias("petal_width"),
... col("_c4").alias("species"))
>>> vectorAssembler =
>>> VectorAssembler(inputCols=["sepal_length","sepal_width","petal_length","petal_width"],outputCol="feature")
>>> viris_df = vectorAssembler.transform(iris_df)
>>> indexer = StringIndexer(inputCol="species",outputCol="label")
>>> iviris_df = indexer.fit(viris_df).transform(viris_df)
>>> iviris_df.take(1)
[Row(sepal_length=5.1, sepal_width=3.5, petal_length=1.4,
petal_width=0.2, species='Iris-setosa', feature=DenseVector([5.1, 3.5,
1.4, 0.2]), label=0.0)]
```

#### Classification

- Split data into training data and testing data
- Create a classifier
- Create a model by fitting the classifier on training data
- Run the model on the test data

```bash
>>> from pyspark.ml.classification import NaiveBayes
>>> from pyspark.ml.evaluation import MulticlassClassificationEvaluator
>>> splits = iviris_df.randomSplit([0.6,0.4],1)
>>> train_df = splits[0]
>>> test_df = splits[1]
>>> nb = NaiveBayes(modelType="multinomial")
>>> nbmodel = nb.fit(train_df)
2018-07-09 17:08:02 WARN  BLAS:61 - Failed to load implementation from:
com.github.fommil.netlib.NativeSystemBLAS
2018-07-09 17:08:02 WARN  BLAS:61 - Failed to load implementation from:
com.github.fommil.netlib.NativeRefBLAS
>>> predictions_df = nbmodel.transform(test_df)
>>> predictions_df.take(1)
[Row(sepal_length=4.5, sepal_width=2.3, petal_length=1.3,
petal_width=0.3, species='Iris-setosa', features=DenseVector([4.5, 2.3,
1.3, 0.3]), label=0.0, rawPrediction=DenseVector([-10.3605, -11.0141,
-11.7112]), probability=DenseVector([0.562, 0.2924, 0.1456]),
prediction=0.0)]
```

#### Evaluation

- Create an evaluator
- Evaluate the prediction data sets

```bash
>>> evaluator =
>>> MulticlassClassificationEvaluator(labelCol="label",predictionCol="prediction",metricName="accuracy")
>>> nbaccuracy = evaluator.evaluate(predictions_df)
>>> nbaccuracy
0.5862068965517241
```

### Multilayer Perceptron

- Neural network
- The first layer has the same number of nodes as there are inputs
    + Iris UCI data set has four measures => four nodes
- The last element should have the same number of neurons as there are
  types of outputs.
    + Three types of Iris species => last row will be three
- Layers in between help the multi-layer perceptron learn how to
  classify correctly

```bash
>>> from pyspark.ml.classification import MultilayerPerceptronClassifier
>>> layers = [4,5,5,3]
>>> mlp = MultilayerPerceptronClassifier(layers=layers,seed=1)
>>> mlp_model = mlp.fit(train_df)
>>> mlp_predictions = mlp_model.transform(test_df)
>>> mlp_evaluator =
>>> MulticlassClassificationEvaluator(metricName="accuracy")
>>> mlp_accuracy = mlp_evaluator.evaluate(mlp_predictions)
>>> mlp_accuracy
0.9482758620689655
```

### Decision Trees

```bash
>>> from pyspark.ml.classification import DecisionTreeClassifier
>>> dt = DecisionTreeClassifier(labelCol="label",featuresCol="features")
>>> dt_model = dt.fit(train_df)
>>> dt_predictions = dt_model.transform(test_df)
>>> dt_evaluator =
>>> MulticlassClassificationEvaluator(metricName="accuracy")
>>> dt_accuracy = dt_evaluator.evaluate(dt_predictions)
>>> dt_accuracy
0.9310344827586207
```


## Regression

- Algorithms
    + Linear Regression
    + Decision tree regression
    + Gradient-boosted tree regression
        * Can require significantly more time to build the models


# Spark Shell

- `bin/spark-shell --master "local[4]"`
    + the `--master` option specifies the master URL for a distributed
      cluster, or `local` to run locally with one thread, or `local[N]`
      to run locally with N threads.

# Cluster Mode

## Overview

### Components

- Spark applications run as independent sets of processes on a cluster,
  coordinated by the `SparkContext` object in your main program (called
  the `driver program`)
- The SparkContext can connect to several types of *cluster managers*
  (either Spark's own standalone cluster manager, Mesos or YARN), which
  allocate resources across applications
- Once connected, Spark acquires `executors` on nodes in the cluster,
  which are processes that run computations and store data for your
  application.
- Next, it sends your application code (defined by JAR or Python files
  passed to SparkContext) to the executors.
- Finally, SparkContet sends `tasks` to the executors to run.

![Spark-architecture](https://spark.apache.org/docs/latest/img/cluster-overview.png)

Useful things about this architecture:

- Each application gets its own executor processes, which stay up for
  the duration of the whole application and run tasks in multiple
  threads.
    + isolating applications form each other
        * scheduling side (each driver schedules its own tasks)
        * executor side (tasks from different applications run in
          different JVMs)
    + however, it means that data cannot be shared across different
      Spark applications without writing it to an external storage
      system.
- Spark is agnostic to the underlying cluster manager.
- the driver program must listen for and accept incoming connections
  from its executors throughout its lifetime
    + the driver program must be network addressable from the worker
      nodes.
- Because the driver schedules tasks on the cluster, it should be run
  close to the worker nodes, preferably on the same local area network.
    + If you'd like to send requests to the cluster remotely, it's
      better to open an RPC to the drier and have it submit operations
      from nearby than to run a drier far away from the worker nodes.

## Cluster Manager Types

### Standalone Mode

#### Introduction

- A simple cluster manager included with Spark that makes it easy to set
  up a cluster.
- Launching
    + starting a master and workers manually
    + using launch scripts

#### Installing Spark Standalone to a cluster

- place a compiled version of Spark on  each node on the cluster

#### Starting a cluster manually

- master
    + `$ sbin/start-master.sh`
    + once started, the master will print out a `spark://HOST:PORT` URL
      for itself, which you can use to connect workers to it, or pass as
      the "master" argument to SparkContect.
    + master web-ui: http://localhost:8080
- workers
    + `$ sbin/start-slave.sh <master-spark-URL>`

#### Using launch scripts

- To launch a Spark standalone cluster with the launch scripts, you
  should create a file called `conf/slaves` in your Spark directory,
  which must contain the hostnames of all the machines where you intend
  to start Spark workers, one per line.
    + if `conf/slaves` does not exist, the launch scripts defaults to a
      single machine (localhost)
    + the master machine accesses each of the worker machines via ssh
- the following scripts must run on the master machine

| script               | description                                                               |
| -                    | -                                                                         |
| sbin/start-master.sh | starts a master instance on the machine the script is executed on         |
| sbin/start-slaves.sh | starts a slave instance on each machine specified in the conf/slaves file |
| sibn/start-slave.sh  | starts a slave instance on the machine the script is executed on          |
| sbin/start-all.sh    | starts both a master and a number of slaves as described above            |
| sbin/stop-master.sh  | stops the master that was started via the sbin/start-master.sh            |
| sbin/stop-slaves.sh  | stops the slaves that was specified in conf/slaves                        |
| sbin/stop-all.sh     | stops both the master and slaves                                          |

- You can optionally configure the cluster further by setting
  environment variables in `conf/spark-env.sh`
    + https://spark.apache.org/docs/latest/spark-standalone.html

#### Connecting an application to the cluster

- simply pass the `spark://IP:PORT` URL of the master as to the
  SparkContext constructor
- to run an interactive Spark shell against the cluster
    + `bin/spark-shell --master spark://IP:PORT`
    + option `--total-executor-cores <numCores>` to control the number
      of cores that spark-shell uses on the cluster

#### Launching Spark applications

- using spark-submit script
- two deploy modes
    + `client` mode:
        * the driver is launched in the same process as the client that
          submits the application
    + `cluster` mode
        * the driver is launched from one of the Worker processes inside
          the cluster, and the client process exits as soon as it
          fulfills its responsibility of submitting the application
          without waiting for the application to finish
- if your application is launched through spark-submit, then the
  application jar is automatically distributed to all worker nodes
    + for any additional jars that your application depends on, you
      should specify them through the --jars flag using comma as a
      delimiter (e.g. --jars jar1,jar2)
- Spark configuration
    + https://spark.apache.org/docs/latest/configuration.html
- standalone cluster mode supports restarting your application
  automatically if it exited with non-zero exit code
    + pass the flag `--supervise` to spark-submit when launching your
      application
    + kill an application that is failing repeatedly
        * `bin/spark-class org.apache.spark.deploy.Client kill <master url> <driver ID>`
        * you can find the driver ID through the master web ui http://<master url>:8080



### Apache Mesos

- https://spark.apache.org/docs/latest/running-on-mesos.html

### Hadoop YARN

- https://spark.apache.org/docs/latest/running-on-yarn.html

### Kubernetes

- https://spark.apache.org/docs/latest/running-on-kubernetes.html

## Glossary

| Term            | Meaning                                                                                                                                                                                           |
| -               | -                                                                                                                                                                                                 |
| Application     | User program built on Spark. Consist of a *driver program* and *executors* on the cluster                                                                                                         |
| Application jar | A jar containing the user's Spark application.                                                                                                                                                    |
| Driver program  | The process running the main() function of the application and creating the SparkContext                                                                                                          |
| Cluster manager | An external service for acquiring resources on the cluster (e.g. standalone manager, Mesos, YARN)                                                                                                 |
| Deploy mode     | distinguishes where the driver process runs, in "cluster" mode, the framework launches the drier inside of the cluster. In "client" mode the submitter launches the driver outside of the cluster |
| Worker node     | any node that can run application code in the cluster                                                                                                                                             |
| Executor        | A process launched for an application on a worker node, that run tasks and keeps data in memory or disk storage across them. Each application has its own executors                               |
| Task            | a unit of work that will be sent to one executor                                                                                                                                                  |
| Job             | A parallel computation consisting of multiple tasks that gets spawned in response to a Spark action (e.g. save, collect)                                                                          |
| Stage           | Each job gets divided into smaller sets of tasks called stages that depend on each other (similar to the map and reduce stages in MapReduce)                                                      |

# Configuration

- https://spark.apache.org/docs/latest/configuration.html

## Spark Properties

- priority order
    + SparkConf take highest precedence
    + flags passed to spark-submit or spark-shell
    + options in the spark-defaults.conf file

### Programmatically loading Spark properties

- Spark properties control most application settings and are configured
  separately for each application
    + it can be set directly on a `SparkConf` passed to your
      `SparkContext`

```scala
val conf = new SparkConf()
             .setMaster("local[2]")
             .setAppName("CountingSheep")
val sc = new SparkContext(conf)
```

### Dynamically loading Spark properties

```scala
// empty conf
val sc = new SparkContext(new SparkConf())
```

- Supply configuration values at runtime
    + `bin/spark-submit` reads configuration options from
      `conf/spark-default.conf`
    + flags passed to `bin/spark-submit`

```
./bin/spark-submit --name "My app" --master local[4] --conf spark.eventLog.enabled=false
  --conf "spark.executor.extraJavaOptions=-XX:+PrintGCDetails -XX:+PrintGCTimeStamps" myApp.jar
```

### Viewing Spark properties

- http://<driver>:4040
    + lists Spark properties in the "Environment" tab
    + note that only values explicitly specified through
      `spark-defaults.conf, SparkConf`, or the command line will appear
    + For all other configuration properties, you can assume the default
      value is used

### Available Properties

- https://spark.apache.org/docs/latest/configuration.html#available-properties

#### Cluster Managers

- https://spark.apache.org/docs/latest/configuration.html#cluster-managers

## Environment Variables

- `conf/spark-env.sh`
- since `conf/spark-env.sh` is a shell script, some of these can be set
  programmatically
    + you might compute `SPARK_LOCAL_IP` by looking up the IP of a
      specific network interface
- Pay attention for YARN cluster mode
    + https://spark.apache.org/docs/latest/running-on-yarn.html#spark-properties

## Configuring Logging

- `conf/log4j.properties`

## Overriding configuration directory

- `export SPARK_CONF_DIR=...`

## Inheriting Hadoop Cluster Configuration

- If you plan to read and write from HDFS using Spark, there are two
  Hadoop configuration files that should be included on Spark's
  classpath
    + `hdfs-site.xml` which provides default behaviors for the HDFS
      client
    + `core-site.xml` which sets the default filesystem name
- To make these files visible to Spark, set `HADOOP_CONF_DIR` in
  `conf/spark-env.sh` to a location containing the configuration files

# Submitting Applications

- https://spark.apache.org/docs/latest/submitting-applications.html
- `spark-submit` script in Spark's `bin` directory

## Bundling your application's dependencies

- if your code depends on other projects, you will need to package them
  alongside your application in order to distribute the code to a Spark
  cluster.
    + create an assembly jar (or "uber" jar) containing your code and
      its dependencies
    + both sbt and Maven have assembly plugins
    + when creating assembly jars, list Spark and Hadoop as `provided`
      dependencies => these need not be bundled since they are provided
      by the cluster manager at runtime
- For Python, you can use the `--py-files` argument of `spark-submit` to
  add `.py, .zip or .egg` files

## Launching with spark-submit

```
./bin/spark-submit \
  --class <main-class> \
  --master <master-url> \
  --deploy-mode <deploy-mode> \
  --conf <key>=<value> \
  ... # other options
  <application-jar> \
  [application-arguments]
```

- Commonly used options
    + `--class`: the entry point for your application (e.g.
      `org.apache.spark.examples.SparkPi`)
    + `--master`: the master URL for the cluster (e.g.
      `spark://192.168.0.45:7077`)
    + `--deploy-mode`: whether to deploy your driver on the worker nodes
      (`cluster`) or locally as an external client (`client`) (default:
      `client`)
    + `--conf`: arbitrary Spark configuration property in key=value
      format. For values that contain spaces wrap "key=value" in quotes
    + `application-jar`: path to a bundled jar including your
      application and all dependencies. The URL must be globally visible
      inside of your cluster, for instance, and `hdfs://` path or a
      `file://` path that is present on all nodes
    + `application-arguments`: arguments passed to the main method of
      your main class, if any


```
# Run application locally on 8 cores
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master local[8] \
  /path/to/examples.jar \
  100

# Run on a Spark standalone cluster in client deploy mode
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master spark://207.184.161.138:7077 \
  --executor-memory 20G \
  --total-executor-cores 100 \
  /path/to/examples.jar \
  1000

# Run on a Spark standalone cluster in cluster deploy mode with supervise
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master spark://207.184.161.138:7077 \
  --deploy-mode cluster \
  --supervise \
  --executor-memory 20G \
  --total-executor-cores 100 \
  /path/to/examples.jar \
  1000

# Run on a YARN cluster
export HADOOP_CONF_DIR=XXX
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master yarn \
  --deploy-mode cluster \  # can be client for client mode
  --executor-memory 20G \
  --num-executors 50 \
  /path/to/examples.jar \
  1000

# Run a Python application on a Spark standalone cluster
./bin/spark-submit \
  --master spark://207.184.161.138:7077 \
  examples/src/main/python/pi.py \
  1000

# Run on a Mesos cluster in cluster deploy mode with supervise
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master mesos://207.184.161.138:7077 \
  --deploy-mode cluster \
  --supervise \
  --executor-memory 20G \
  --total-executor-cores 100 \
  http://path/to/examples.jar \
  1000

# Run on a Kubernetes cluster in cluster deploy mode
./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master k8s://xx.yy.zz.ww:443 \
  --deploy-mode cluster \
  --executor-memory 20G \
  --num-executors 50 \
  http://path/to/examples.jar \
  1000
```

## Master URLs

| Master URL                      | Meaning                                                                                                                                                                                                                                                                                                       |
| -                               | -                                                                                                                                                                                                                                                                                                             |
| local                           | Run Spark locally with one worker thread (i.e. no parallelism at all)                                                                                                                                                                                                                                         |
| local[K]                        | Run Spark locally with K worker threads (ideally, set this to the number of cores on your machine)                                                                                                                                                                                                            |
| local[K,F]                      | Run Spark locally with K worker threads and F maxFailures                                                                                                                                                                                                                                                     |
| local[*]                        | Run Spark locally with as many worker threads as logical cores on your machine                                                                                                                                                                                                                                |
| local[*,F]                      | Run Spark locally with as many worker threads as logical cores on your machine and F maxFailures                                                                                                                                                                                                              |
| spark://HOST:PORT               | Connect to the given Spark standalone cluster master. The port must be whichever one your master is configured to use, which is 7077 by default                                                                                                                                                               |
| spark://HOST1:PORT1,HOST2:PORT2 | Connect to the given Spark standalone cluster with standby masters with Zookeeper. The list must have all the master hosts in the high availability cluster set up with Zookeeper. The port must be whichever each master is configured to use                                                                |
| mesos://HOST:PORT               | Connect to the given Mesos cluster. The port must be whichever one your is configured to use, which is 5050 by default. Or, for a Mesos cluster using Zookeeper, use `mesos://zk://...` to submit with `--deploy-mode` `cluster`, the HOST:PORT should be configured to connect to the MesosClusterDispatcher |
| yarn                            | Connect to a YARN cluster in client or cluster mode depending on the value of `--deploy-mode`. The cluster location will be found based on the HADOOP_CONF_DIR or  YARN_CONF_DIR variable                                                                                                                     |
| k8s://HOST:PORT                 | Connect to a Kubernetes cluster in cluster mode. Client mode is currently unsupported and will be supported in the future releases.                                                                                                                                                                           |


## Loading configuration from a file

- `conf/spark-defaults.conf`
- configuration values explicitly set on a `SparkConf` take the highest
  precedence, then flags passed to `spark-submit`, then values in the
  default file
- print debugging information to know where configuration options are
  coming from by running `spark-submit` with the `--verbose` option

# Monitoring

- https://spark.apache.org/docs/latest/monitoring.html
- There are several ways to monitor Spark applications
    + web UIs
    + REST API metrics
    + external instrumentation

## Web interfaces

- every SparkContext launches a web UI, by default on port 4040
    + a list of scheduler stages and tasks
    + a summary of RDD sizes and memory usage
    + environmental information
    + information about the running executors
- if multiple SparkContexts are running on the same host, they will bind
  to successive ports beginning with 4040 (4041, 4042, etc.)
- Viewing after the fact (history data): set `spark.eventLog.enabled` to
  true before starting the application
    + this configures Spark to log Spark events that encode the
      information displayed in the UI to persisted storage

### Viewing after the fact

- if `spark.eventLog.enabled` is true
- start the history server: `sbin/start-history-server.sh`
    + this creates a web interface at `http://<server-url>:18080` by
      default, listing incomplete and completed applications and
      attempts
- When using the file-system provider class `spark.history.provider` the
  base logging directory must be supplied in the
  `spark.history.fs.logDirectory`
- `spark.eventLog.dir hdfs://namenode/path/to/log/dir`

### Environment Variables

- https://spark.apache.org/docs/latest/monitoring.html

### Spark configuration options

- https://spark.apache.org/docs/latest/monitoring.html
- The time between incomplete application updates is defined by the
  interval between checks for changed files
    + `spark.history.fs.update.interval`
- One way to signal the completion of a Spark job is to stop the Spark
  Context explicitly `sc.stop()`

## REST API

- in addition to viewing the metrics in the UI, they are also available
  as JSON
    + developers can create new visualizations and monitoring tools for
      Spark
- JSON is available for both running applications, and in the history
  server
- the endpoints are mounted at `/api/v1`
    + `http://<server-url>:18080/api/v1`
    + `http://localhost:4040/api/v1`

### Metrics

- Spark has a configuratble metrics system based on the Dropwizard
  Metrics Library
- This allows users to report Spark metrics to a variety of sinks
  including HTTP, JMX, and CVS files
- The metric system is configured via a configuration file that Spark
  expects to be present at `$SPARK_HOME/conf/metrics.properties`
    + A custom file location can be specified via the
      `spark.metrics.con` configuration property
    + By default, the root namespace used for driver or executor metrics
      is the value of `spark.app.id`
    + However, often times, users want to be able to track the metrics
      across apps for driver and executors, which is hard to do with
      application ID (i.e. `spark.app.id`) since it changes with every
      invocation of the app.
        * For such cases, a custom namespace can be specified for
          metrics reporting using `spark.metrics.namespace`
          configuration property
        * If users wanted to set the metrics namespace to the name of
          the application, they can set the `spark.metrics.namespace`
          property to a value like `${spark.app.name}`
- Spark's metrics are decoupled into different instances corresponding
  to Spark components.
    + Within each instance, you can configure a set of sinks to which
      metrics are reported.
    + The following instances are currently supported:
        * `master`: the Spark standalone master process
        * `applications`: a component within the master which reports on
          various applications
        * `worker`: a Spark standalone worker process
        * `executor`: a Spark executor
        * `driver`: the Spark driver process (the process in which your
          SparkContext is created)
        * `shuffleService`: the Spark shuffle service
    + Each instance can report to zero or more sinks. Sinks are
      contained in the `org.apache.spark.metrics.sink` package
        * `ConsoleSink`: logs metrics information to the console
        * `CSVSink`: exports metrics data to CSV files at regular
          intervals
        * `JmxSink`: Registers metrics for viewing in a JMX console
        * `MetricsServlet`: adds a servlet within the existing Spark UI
          to serve metrics data as JSON data
        * `GraphiteSink`: sends metrics to a Graphite node
        * `Slf4jSink`: Sends metrics to slf4j as log entries
        * `StatsdSink`: sends metrics to a StatsD node
- The syntax of the metrics configuration file is defined in an example
  configuration file, `conf/metrics.properties.template`

## Advanced Instrumentation

- cluster-wide monitoring tools, such as Ganglia, can provide insight
  into overall cluster utilization and resource bottlenecks.
- OS profiling tools such as dstat, iostat, and iotop can provide
  fine-grained profilling on individual nodes
- JVM utilities such as `jstack` for providing stack traces, `jmap` for
  creating heap-dumps, `jstat` for reporting time-series statistics and
  `jconsole` for visually exploring various JVM properties are useful
  for those comfortable with JVM internals.

# Tuning Guide - Optimization

- https://spark.apache.org/docs/latest/tuning.html
- Spark programs can be bottlenecked by any resource in the cluster:
  CPU, network bandwidth, or memory.
    + most often, if the data fits in memory, the bottleneck is network
      bandwidth, but sometimes, you also need to do some tuning, such as
      storing RDDs in serialized form, to decrease memory usage
- Data serialization => crucial for good network performance and reduce
  memory use
- Memory tuning

## Data Serialization

- Serialization plays an important role in the performance of any
  distributed application
    + serialization => slow down computation, but save memory
- Two serialization libraries
    + Java serialization
        * by default, Spark serializes objects using Java's
          `ObjectOutputStream` framework
        * slow
    + Kryo serialization
        * Kryo library: `https://github.com/EsotericSoftware/kryo`
        * faster, less flexible (does not support all `Serializable`
          types)
        * requires you to register the classes you'll use in the program
          in advance for best performance
        * initializing your job with a SparkConf and calling
        * `conf.set("spark.serializer", "org.apache.spark.serializer.KryoSerializer")`
        * to register your own custom classes with Kryo, use the
          `registerKryoClasses` method

```scala
val conf = new SparkConf().setMaster(...).setAppName(...)
conf.registerKryoClasses(Array(classOf[MyClass1], classOf[MyClass2]))
val sc = new SparkContext(conf)
```

- if your objects are large, you may also need to increase the
  `spark.kryoserializer.buffer` config. This value needs to be large
  enough to hold the largest object you will serialize
- if you don't register  your custom classes, Kryo still work, but it
  will have to store the full class name with each object, which is
  wasteful

## Memory tuning

### Introduction

- there are three considerations in tuning memory usage
    + the amount of memory used by your objects (you may want your
      entire dataset to fit in memory)
    + the cost of accessing those objects
    + the overhead of garbage collection (if you have high turnover in
      terms of objects)
- by default, Java objects are fast to access, but can easily consume a
  factor of 2-5x more space than the "raw" data inside their fields.
  This is due to several reasons
    + each distinct Java object has an "object header", which is about
      16 bytes and contains information such as a pointer to its class.
    + Java `String`s have about 40 bytes of overhead over the raw string
      data (since they store it in an array of `Char`s and keep extra
      data such as the length), and store each character as two bytes
      due to `String`'s internal usage of UTF-16 encoding. Thus a
      10-character string can easily consume 60 bytes.
    + Common collection classes, such as `HashMap` and `LinkedList`, use
      linked data structures, where there is a "wrapper" object for each
      entry (e.g. Map.Entry). This object not only has a header, but
      also pointers (typically 8 bytes each) to the next object in the
      list.
    + Collections of primitive types often store them as "boxed" objects
      such as `java.lang.Integer`

### Memory Management Overview

- memory usage in Spark: execution and storage
    + execution memory: used for computation in shuffles, joins,
      aggregations
    + storage memory: used for caching and propagating internal data
      across the cluster
- execution and storage share a unified region (M)
    + when no execution memory is used, storage can acquire all the
      available memory and vice versa.
    + execution may evict storage if necessary, but only until total
      storage memory usage falls under a certain threshold (R).
        * in other words, `R` describes a subregion within `M` where
          cached blocks are never evicted
    + storage may not evict execution due to complexities in
      implementation
- this design ensure several desirable properties
    + applications that do not use caching can use the entire space for
      execution, obviating unnecessary disk spills
    + applications that do use caching can reserve a minimu storage
      space (R) where their data blocks are immune to being evicted.
    + this approach provides reasonable out-of-the-box performance for a
      variety of workloads without requiring user expertise of how
      memory is divided internally
- defaults
    + `spark.memory.fraction` expresses the size of `M` as a fraction of
      the JVM heap space (default 0.6). The rest of the space (40%) is
      reserved for user data structures, internal metadata in Spark, and
      safeguarding against OOM errors in the case of sparse and
      unusually large records
        * this value should be set to fit this amount of heap space
          comfortably within the JVM's old or "tenured" generation
    + `spark.memory.storageFraction` expresses the size of `R` as a
      fraction of `M` (default 0.5). `R` is the storage space within `M`
      where cached blocks immune to being evicted by execution

### Determining Memory Consumption

- The best way to size the amount of memory consumption a dataset will
  require is:
    + create an RDD, put it into cache
    + look at the "Storage" page in the web UI
    + the page will tell you how much memory the RDD is occupying
- To estimate the memory consumption of a particular object, use
  `SizeEstimator`'s `estimate` method.
    + this is useful for experimenting with different data layouts
    + determining the amount of space a broadcast variable will occupy
      on each executor heap

### Tuning Data Structures

- avoid Java features that add overhead, such as pointer-based data
  structures and wrapper objects
- Several ways
    + Design your data structures to prefer arrays of objects, and
      primitive types, instead of the standard Java or Scala collection
      classes (e.g. HashMap)
        * the `fastutil` library provides convenient collection classes
          for primitive types that are compatible with the Java standard
          library
        * http://fastutil.di.unimi.it/
    + Avoid nested structures with a lot of small objects and pointers
      when possible
    + Consider using numeric IDs or enumeration objects instead of
      strings for keys
    + If you have less than 32 GB of RAM, set the JVM flag
      `-XX:+UseCompressedOops` to make pointers be four bytes instead of
      eight. You can add these options in `spark-env.sh`

### Serialized RDD Storage

- using the serialized StorageLevels in the RDD persistence API
    + https://spark.apache.org/docs/latest/rdd-programming-guide.html#rdd-persistence
    + such as `MEMORY_ONLY_SER` => Spark will then store each RDD
      partition as one large byte array
- using Kryo library

### Garbage Collection Tuning

#### Introduction

- JVM garbage collection can be a problem when you have large "churn" in
  terms of the RDDs stored by your program.
    + it is usually not a problem in programs that just read an RDD once
      and then run many operations on it
    + when Java needs to evict old objects to make room for new ones, it
      will need to trace through all your Java objects and find the
      unused ones => the cost of garbage collection is proportional to
      the number of Java objects => using data structures with fewer
      objects (e.g. an array of `Int`s instead of a `LinkedList`)
      greatly lowers this cost
    + an even better method is to persist objects in serialized form, as
      described above: now there will be only one object (a byte array)
      per RDD partition
- GC can be a problem due to interference between your tasks' working
  memory (the amount of space needed to run the task) and the RDDs
  cached on your nodes

### Measuring the impact of GC

- adding `-verbose:gc -XX:+PrintGCDetails -XX:+PrintGCTimeStamps` to
  Java options
    + next time your Spark job is run, you will see messages printed in
      the worker's logs each time a garbage collection occurs.
    + these logs will be on your cluster's worker nodes (in the `stdout`
      files in their work directories), not on your driver program

### Advanced GC Tuning

#### Memory management in the JVM

- Java Heap space is divided in to two regions Young and Old
    + The Young generation is meant to hold short-lived objects
    + the Old generation is intended for objects with longer lifetimes
- The Young generation is further divided into three regions [Eden,
  Survivor1, Survivor2]
- A simplified description of the garbage collection procedure
    + when Eden is full, a minor GC is run on Eden and objects that are
      alive from Eden and Survivor1 are copied to Survivor2
    + if an object is old enough or Survivor2 is full, it is moved to
      Old
    + when Old is close to full, a full GC is invoked

#### GC tuning

- http://www.oracle.com/technetwork/java/javase/gc-tuning-6-140523.html
- goal of GC tuning in Spark is to ensure that only long-lived RDDs are
  stored in the Old generation and that the Young generation is
  sufficiently sized to store short-lived objects
   + avoid full GCs
- some steps can take
    + if a full GC is invoked multiple times => there isn't enough
      memory available for executing tasks
    + if there are too many minor collections but not many major GCs =>
      allocating more memory for Eden
        * set the Young generation using the option `-Xmn=4/3*E` with E
          is the size of Eden
    + if the Old generation is close to being full, reduce the amount of
      memory used for caching by lowering `spark.memory.fraction`
    + try the G1GC garbage collector with `-XX:+UseG1GC`
        * with large executor heap sizes, it may be important to
          increase the G1 regions size with `-XX:G1HeapRegionSize`
        * http://www.oracle.com/technetwork/articles/java/g1gc-1984535.html
    + as an example, if your task is reading data from HDFS, the amount
      of memory used by the task can be estimated using the size of the
      data block read from HDFS.
        * the size of a decompressed block is often around 3 times the
          size of the block
        * so if we wish to have 4 tasks' worth of working space, and the
          HDFS block size is 128 MB, we can estimate size of Eden to be
          4*3*128 MB

### Other Considerations

#### Level of Parallelism

- clusters will not be fully utilized unless you set the level of
  parallelism for each operation high enough.
- Spark automatically sets the number of "map" tasks to run on each file
  according to its size
    + you can control it through optional parameters to
      `SparkContext.textFile`, etc.
- For distributed "reduce" operations, such as `groupByKey` and
  `reduceByKey`, it uses the largest parent RDD's number of partitions
- You can pass the level of parallelism as a second argument
    + https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.rdd.PairRDDFunctions
- Or you can set the config property `spark.default.parallelism` to
  change the default => recommended: 2-3 tasks per CPU core

#### Memory Usage of Reduce Tasks

- increase the level of parallelism

#### Broadcasting Large Variables

- https://spark.apache.org/docs/latest/rdd-programming-guide.html#broadcast-variables
- available in SparkContext
- if your tasks use any large object from the driver program inside of
  them (e.g. a static lookup table), consider turning it into a
  broadcast variable
- in general tasks larger than about 20 KB are probably worth optimizing

#### Data locality

- if data and code are separated, one must move to the other
    + typically it is faster to ship serialized code from place to place
      than a chunk of data because code size is much smaller than data
- data locality is how close data is to the code processing it. There
  are several levels of locality based on the data's current location.
  In order from closest to farthest:
    + `PROCESS_LOCAL` data is in the same JVM as the running code
        * this is the best locality possible
    + `NODE_LOCAL` data is on the same node
        * examples might be in HDFS on the same node, or in another
          executor on the same node
    + `NO_PREF` data is accessed equally quickly from anywhere and has
      no locality preference
    + `RACK_LOCAL` data is on the same rack of servers.
    + `ANY` data is elsewhere on the network and not in the same rack
- in situations where there is no unprocessed data on any idle executor,
  Spark switches to lower locality levels


# Job Scheduling

- https://spark.apache.org/docs/latest/job-scheduling.html

## Overview

- The cluster managers that Spark runs on provide facilities for
  scheduling across applications
    + Each Spark application (instance of SparkContext) runs an
      independent set of executor processes
- Within each Spark application, multiple "jobs" (Spark actions) may be
  running concurrently if they were submitted by different threads
    + this is common if your application is serving requests over the
      network
    + Spark includes a fair scheduler to schedule resources within each
      SparkContext

## Scheduling Across Applications

### Dynamic Resource Allocation

#### Configuration and Setup

Something

#### Resource Allocation Policy

##### Request Policy

Something

##### Remove Policy

Something

#### Graceful Decommission of Executors

Something

## Scheduling Within an Application

### Fair Scheduler Pools

Something

### Default Behavior of Pools

Something

### Configuring Pool Properties

Something

# Security

- https://spark.apache.org/docs/latest/security.html

# Coding

## Resources

- API Docs
    + https://spark.apache.org/docs/latest/api
- AMP Camps
    + http://ampcamp.berkeley.edu/
- Code Examples
    + http://spark.apache.org/examples.html
    + https://github.com/apache/spark/tree/master/examples

## R accesses MLlib

```r
iris_data <- createDataFrame(iris)
model <- glm(Sepal_Length ~ Sepal_Width + Species, data = iris_data, family = "gaussian")
summary(model)
```

# References

[streaming]: https://www.linkedin.com/pulse/spark-streaming-vs-flink-storm-kafka-streams-samza-choose-prakash
[sql]: https://www.dezyre.com/article/spark-sql-vs-apache-drill-war-of-the-sql-on-hadoop-tools/234
[genomics]: https://aws.amazon.com/blogs/big-data/will-spark-power-the-data-behind-precision-medicine/
