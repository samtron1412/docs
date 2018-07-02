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

# Hardware Provisioning

- https://spark.apache.org/docs/latest/hardware-provisioning.html

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


# Spark SQL, Datasets, and DataFrames

- https://spark.apache.org/docs/latest/sql-programming-guide.html

# Spark Streaming

- https://spark.apache.org/docs/latest/streaming-programming-guide.html

# MLlib

- https://spark.apache.org/docs/latest/ml-guide.html

# GraphX

- https://spark.apache.org/docs/latest/graphx-programming-guide.html

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

- configuration values explicitly set on a `SparkConf` take the highest
  precedence, then flags passed to `spark-submit`, then values in the
  default file
- print debugging information to know where configuration options are
  coming from by running `spark-submit` with the `--verbose` option

# Monitoring

- https://spark.apache.org/docs/latest/monitoring.html
-

# Tuning Guide - Optimization

- https://spark.apache.org/docs/latest/tuning.html


# Job Scheduling

- https://spark.apache.org/docs/latest/job-scheduling.html

# Security

- https://spark.apache.org/docs/latest/security.html

# Coding

- API Docs
    + https://spark.apache.org/docs/latest/api
- AMP Camps
    + http://ampcamp.berkeley.edu/
- Code Examples
    + http://spark.apache.org/examples.html
    + https://github.com/apache/spark/tree/master/examples

# References

[streaming]: https://www.linkedin.com/pulse/spark-streaming-vs-flink-storm-kafka-streams-samza-choose-prakash
[sql]: https://www.dezyre.com/article/spark-sql-vs-apache-drill-war-of-the-sql-on-hadoop-tools/234
