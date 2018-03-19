[TOC]

# Overview

# Apache Kafka

## Introduction

Apache Kafka is an open-source *distributed stream processing* software

- Written in Scala and Java
- Aiming to provide a unified, high-throughput, low-latency platform for
  handling real-time data feeds
    + Using storage layer: massively scalable pub/sub/message queue
      designed as a distributed transaction log
    + Influenced by "*transaction log*" in database
- Features or capabilities
    + Publish and subscribe to streams of *records*
    + Store streams of records in a fault-tolerant way
    + Process streams of records as they occur
- Applications
    + Building *real-time streaming data* pipelines that reliably get
      data between systems or applications
    + Building real-time streaming applications that transform or react
      to the streams of data
- Architecture
    + Kafka is run as a *cluster* on one or more servers
    + The Kafka cluster stores streams of records in categories called
      *topics*
    + Each record consists of a key, a value, and a timestamp
- APIs: 4 cores
    + The *Producer API* allows an application to publish a stream of
      records to one or more Kafka topics.
    + The *Consumer API* allows an application to subscribe to one or
      more topics and process the stream of records produced to them.
    + The *Streams API* allows an application to act as a stream
      processor, consuming an input stream from one or more topics and
      producing an output stream to one or more output topics,
      effectively transforming the input streams to output streams.
    + The *Connector API* allows building and running reusable producers
      or consumers that connect Kafka topics to existing applications or
      data systems. For example, a connector to a relational database
      might capture every change to a table.
- Communication between the clients and the servers
    + a simple, high-performance, language agnostic *TCP protocol*
    + this protocol is versioned and maintains backwards compatibility
      with older version
    + Java client is provided, but clients are available in many
      languages

![Kafka APIs](../../../graphic/career/jpl/kafka-apis.png)

## Topics and Logs

+ A topic is a category or feed name to which records are published.
    * Topics are always multi-subscriber
    * A topic can have zero, one, or many consumers that subscribe to
      the data written to it
+ For each topic, the cluster maintains a *partitioned log*
    * Each partition is an ordered, immutable sequence of records that
      is continually appended to - a structured commit log
    * The records in the partitions are each assigned a sequential id
      number called the *offset* that uniquely identifies each record
      within the partition.
    * The partitions in the log server several purposes:
        - First, the allow the log to scale beyond a size that will fit
          on a single server
        - Second, they act as the unit of parallelism
+ The cluster retains (keeps) all published records whether or not they
  have been consumed using a configurable retention (possession) period.
    * For example, if the retention policy is set to two days, then for
      the two days after a record is published, it is available for
      consumption, after which it will be discarded to free up space.
    * The only metadata retained on a per-consumer basis is the offset
      or position of that consumer in the log
    * It means the consumers are very cheap

```
Partition 0: | 0 | 1 | 2 | 3 | 4 | 5 | ... <-- Writes
Partition 1: | 0 | 1 | 2 | 3 | 4 | 5 | ... <-- Writes
Partition 2: | 0 | 1 | 2 | 3 | 4 | 5 | ... <-- Writes
Old -----------------------------------> New

Partition 3: | 0 | 1 | 2 | 3 | 4 | 5 | ... <-- Writes (Producers)
               |               |
        Consumer A         Consumer B
        (offset = 0)       (offset = 4)
```


## Distribution

The partitions of the log are distributed over the servers in the
cluster with each server handling data and requests for a share of the
partitions.

- Each partition is replicated across a configurable number of servers
  for fault tolerance.
- Each partition has one server which acts as the "leader" and zero or
  more servers which act as "followers".
    + The leader handles all read and write requests for the partition
    + The followers passively replicate the leader
    + If the leader fails, one of the followers will automatically
      become the new leader
    + Each server acts as a leader for some of its partitions and a
      follower for others so load is well balanced within the cluster

## Producers

Producers publish data to the topics of their choice

- The producer is responsible for choosing which record to assign to
  which partition within the topic
- This can be done in a round-robin fashion simply to balance load or it
  can be done according to some semantic partition function (e.g. based
  on some key in the record)

## Consumers

Consumers label themselves with a *consumer group* name

- Each record published to a topic is delivered to one consumer instance
  within each subscribing consumer group
- Consumer instances can be in separate processes or on separate
  machines
- If all the consumer instances have the same consumer group, then the
  records will effectively be load balanced over the consumer instances
- If all the consumer instances have different consumer groups, then
  each record will be broadcast to all the consumer processes
- The way consumption is implemented is by dividing up the partitions in
  the log over the consumer instances so that each instance is the
  exclusive consumer of a "fair share" of partitions at any point in
  time.
    + This process of maintaining membership in the group is handled by
      the protocol dynamically
    + If new instances join the group they will take over some
      partitions from other members of the group
    + If an instance dies, its partitions will be distributed to the
      remaining instances
- Kafka only provides a total order over records within a partition, not
  between different partitions in a topic.
    + Per-partition ordering combined with the ability to partition data
      by key is sufficient for most applications
    + However, if you require a total order over records this can be
      achieved with a topic that has only one partition -> only one
      consumer process per consumer group

## Guarantees

- Messages sent by a producer to a particular topic partition will be
  appended in the order they are sent.
- A consumer instance sees records in the order they are stored in the
  log.
- For a topic with replication factor N, we will tolerate up to N-1
  server failures without losing any records committed to the log.

## Kafka as a Messaging System

Messaging traditionally has two models

- queuing
    + a pool of consumers may read from a server and each record goes to
      one of them
    + strength: it allows to divide up the processing data over multiple
      consumer instances -> scalability
    + weakness: queues aren't multi-subscriber, once one process reads
      the data it's gone
- publish-subscribe
    + the record is broadcast to all consumers
    + no way of scaling

The consumer group concept in Kafka generalizes these two concepts
- queues: a collection of processes (the members of the consumer group)
- publish-subscribe: to broadcast messages to multiple consumer groups
- both properties: scale processing and multi-subscriber

Kafka has stronger ordering guarantees than a traditional messaging
system.

Traditional queues: records are delivered asynchronously
- the ordering of the records is lost in the presence of parallel
  consumption
- parallelism in Kafka: partitions within the topics
    + assigning the partitions in the topic to the consumers in the
      consumer group so that each partition is consumed by exactly one
      consumer in the group

## Kafka as a Storage system

Any message queue that allows publishing messages decoupled (separated)
from consuming them is effectively acting as a storage system

- Data written to Kafka is written to disk and replicated for fault-
  tolerance
- Kafka allows producers to wait on acknowledgement so that a write
  isn't considered complete until it is fully replicated and guaranteed
  to persist even if the server written to fails
- The disk structures Kafka uses scale well
- storage abilities + allowing the clients to control their read
  position ==> a kind of special purpose distributed filesystem
  dedicated to high-performance, low-latency commit log storage,
  replication, and propagation

## Kafka for Stream Processing

Enable real-time processing of streams

- a stream processor: takes continual streams of data from input topics
  => performs some processing on this input => produces continual
  streams of data to output topics
- simple processing directly using the producer and consumer API
- more complex transformations: *Streams API*
    + handling out-of-order data
    + reprocessing input as code changes
    + performing stateful computations
    + etc.
- Streams API builds on the core primitives Kafka provides
    + It uses the producer and consumer APIs for input
    + Uses Kafka for stateful storage
    + and uses the same group mechanism for fault tolerance among the
      stream processor instances

## Putting the Pieces Together

A streaming platform:

- messaging
- storage
- stream processing

A distributed file system like HDFS allows

- storing static files for batch processing
- storing and processing historical data from the past

A traditional enterprise messaging system allows

- processing future messages that will arrive after subscribing


# Kafka Streams

Kafka Streams is a client library for processing and analyzing data
stored in Kafka.

## Concepts

### Common

- Windowing, stateless processing, stateful processing
- A stream is an unbounded sequence of structured data
  (events/facts/messages/discrete entries). A long-running never-ending
  stream
    + structured data (data record) is immutable
    + a data record = a key-value pair
- A table is a collection of evolving facts
    + A table might be an abstraction over a stream of maybe changes to
      the user profile.
- stream <=> table: duality

### Stream Proccessing Topology

- A stream processing application
    + using the Kafka Streams library
    + it defines its computational logic through one or more processor
      topologies
    + a processor topology is a graph of stream processors (nodes) that
      are connected by streams (edges)
    + a stream processor represents a processing step to transform data
      in streams
        * receiving one input record at a time from its upstream
          processors in the topology,
        * applying its operation to it,
        * and may subsequently produce one or more output records to its
          downstream processors.
        * Two special processors in the topology
            - source processor(s): no upstream processors
                + consuming records from Kafka topics
                + forwarding records to its down-stream processors
            - sink processor(s): no down-stream processors
                + send records from its up-stream processors to a
                  specified Kafka topic
- Kafka Streams offers two ways to define the stream processing topology
    + 2 APIs
    + Streams DSL
        * A high-level API that provides the most common data
          transformation operatiions: `map`, `filter`, `join`, and
          `aggregations`
    + Processor API
        * A low-level API that lets you add and connect processors as
          well as interact directly with state stores
        * more flexible, more manual work
- At runtime, the logical topology is instantiated and replicated inside
  the application for parallel processing.

### Time

Common notions of time in streams:

- Event time: the point in time when an event or data record occurred
- Processing time: the point in time when the event or data record
  happens to be processed by the stream processing application
    + later than the original event time
- Ingestion time: the point in time when an event or data record is
  stored in a topic partition by a Kafka broker

The choice between event-time and ingestion-time is actually done
through the configuration of Kafka

- From Kafka 0.10.x onwards, timestamps are automatically embedded into
  Kafka messages
- The Kafka configuration setting can be specified on the broker level
  or per topic.

Kafka Streams assigns a timestamp to every data record via the
`TimesampExtractor` interface.

- These per-record timestamps describe the progress of a stream with
  regards to time and are leveraged by time-dependent operations such as
  window operations
- As a result, this time will only advance when a new record arrives at
  the processor.
- We call this data-driven time the stream time of the application to
  differentiate with the wall-clock time when this application is
  actually executing

### States

States allow join input streams, group and aggregate data records.

- Kafka Streams provides *state stores* which can be used by stream
  processing applications to store and query data.
- implementing stateful operations
- These state stores can either be
    + a persistent key-value store
    + an in-memory hashmap
    + other convenient data structure
- Kafka Streams offers fault-tolerance and automatic recovery for local
  state stores

Kafka Streams allows direct read-only queries of the state stores by
methods, threads, processes or applications external to the stream
processing application that created the state stores.

- A feature called *Interactive Queries*

### Processing Guarantees

Prior to 0.11.0.0, Kafka only provides *at-least-once* delivery
guarantees

- end-to-end exactly-once semantics: does my stream processing system
  guarantee that each record is processed once and only once, even if
  some failures are encountered in the middle of processing?
- Since the 0.11.0.0 release, Kafka has added support to allow its
  producers to send messages to different topic partitions in a
  transactional and idempotent manner
    + hence, Kafka Streams has added the end-to-end exactly-once
      semantics
    + Kafka Streams guarantees that for any record read from the source
      Kafka topics, its processing results will be reflected exactly
      once in the outputKafka topic as well as in the state stores fro
      stateful operations

## Architecture

### Stream Partitions and Tasks

Kafka Streams uses the concepts of *partitions* and *tasks* as logical
units of its parallelism model based on Kafka *topic partitions*

- each *stream partition* is a totally ordered sequence of data records
  and maps to a Kafka topic partition
- a *data record* in the stream maps to a Kafka *message* from that
  topic
- the *keys* of data records determine the partitioning of data in both
  Kafka and Kafka Streams, i.e. how data is routed to specific
  partitions within topics

An application's processor topology is scaled by breaking it into
multiple tasks
- Each *task* is a part of the processor topology
- Kafka Streams creates a fixed number of tasks based on the input
  stream partitions for the application
    + each task assigned a list of partitions from the input streams
      (Kafka topics)
    + The assignment of partitions to tasks never changes so that each
      task is a fixed unit of parallelism of the application
- Tasks can instantiate their own processor topology based on the
  assigned partitions
    + They also maintain a buffer for each of its assigned partitions
      and process messages one-at-a-time from these record buffers.
    + As a result stream tasks can be processed independently and in
      parallel without manual intervention
- Multiple instances of the application are executed either on the same
  machine, or spread across multiple machines and tasks can be
  distributed automatically by the Kafka Streams library to those
  running application instances.
    + The assignment of partitions to tasks never changes; if an
      application instance fails, all its assigned tasks will be
      automatically restarted on other instances and continue to consume
      from the same stream partitions.

### Threading Model

Kafka Streams allows the user to configure the number of threads that
the library can use to parallelize processing within an application
instance.

- Each thread can execute one or more tasks with their processor
  topologies independently
- There is no shared state among the threads, so no interthread
  coordination is necessary
- The assignment of Kafka topic partitions among the various stream
  threads is transparently handled by Kafka Streams leveraging Kafka's
  coordination functionality

### Local State Stores

The Kafka Streams DSL APIs automatically creates and manages such state
stores when you are calling stateful operators such as `join()` or
`aggregate()`, or when you are windowing a stream

- Every task in Kafka Streams embeds one or more state stores that can
  be accessed via APIs to store and query data required for processing.

### Fault Tolerance

Tasks in Kafka Streams leverage the fault-tolerance capability offered
by the Kafka consumer client to handle failures.

- If a task runs on a machine that fails, Kafka Streams automatically
  restarts the task in one of the remaining running instances of the
  application
- For each state store, it maintains a replicated changelog Kafka topic
  in which it tracks any state updates.
    + These changelog topics are partitioned as well so that each local
      state store instance, and hence the task accessing the store, has
      its own dedicated changelog topic partition.
    + Log compaction is enabled on the changelog topics so that old data
      can be purged safely to prevent the topics from growing
      indefinitely.
    + If tasks run on a machine that fails and are restarted on another
      machine, Kafka Streams guarantees to restore their associated
      state stores to the content before the failure by replaying the
      corresponding changelog topics prior to resuming the processing on
      the newly started tasks.
- The cost of task (re)initialization typically depends primarily on the
  time for restoring the state by replaying the state stores' associated
  changelog topics.
    + To minimize this restoration time, users can configure their
      applications to have *standby replicas* of local states (i.e.
      fully replicated copies of the state).
    + When a task migration happens, Kafka Streams then attempts to
      assign a task to an application instance where such a standby
      replica already exists in order to minimize the task
      (re)initialization cost.
    + `num.standby.replicas`

## Developer Guide

### Writing a Streams Application

#### Libraries and Maven Artifacts

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-streams</artifactId>
    <version>1.0.1</version>
</dependency>
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>1.0.1</version>
</dependency>
```

#### Using Kafka Streams Within Application Code

- First, creating an instance of `KafkaStreams`
    + `KafkaStreams streams = new KafkaStreams(topology, cofigurations)`

```java
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.StreamsBuilder;
import org.apache.kafka.streams.processor.Topology;

// Use the builders to define the actual processing topology, e.g. to specify
// from which input topics to read, which stream operations (filter, map, etc.)
// should be called, and so on.  We will cover this in detail in the subsequent
// sections of this Developer Guide.

StreamsBuilder builder = ...;  // when using the DSL
Topology topology = builder.build();
//
// OR
//
Topology topology = ...; // when using the Processor API

// Use the configuration to tell your application where the Kafka cluster is,
// which Serializers/Deserializers to use by default, to specify security settings,
// and so on.
StreamsConfig config = ...;

KafkaStreams streams = new KafkaStreams(topology, config);
```

- Start the Kafka Streams thread
    + `KafkaStreams#start()`

```java
// Start the Kafka Streams threads
streams.start();
```

- Catch any unexpected exceptions

```java
// Java 8+, using lambda expressions
streams.setUncaughtExceptionHandler((Thread thread, Throwable throwable) -> {
  // here you should examine the throwable/exception and perform an appropriate action!
});


// Java 7
streams.setUncaughtExceptionHandler(new Thread.UncaughtExceptionHandler() {
  public void uncaughtException(Thread thread, Throwable throwable) {
    // here you should examine the throwable/exception and perform an appropriate action!
  }
});
```

- Stop the application instance

```java
// Stop the Kafka Streams threads
streams.close();
```

- To allow you application to gracefully shutdown in response to
  SIGTERM, add a shutdown hook and call `KafkaStreams#close()`

```java
// Add shutdown hook to stop the Kafka Streams threads.
// You can optionally provide a timeout to `close`.
Runtime.getRuntime().addShutdownHook(new Thread(streams::close));

// Java 7
// Add shutdown hook to stop the Kafka Streams threads.
// You can optionally provide a timeout to `close`.
Runtime.getRuntime().addShutdownHook(new Thread(new Runnable() {
  @Override
  public void run() {
      streams.close();
  }
}));
```


## Introduction

### Creating a Streams Application

1) Configure your Kafka Streams application with a *StreamConfig*
   instance

- it is created from a *java.util.Properties* instance
- specify configuration parameters
    + APPLICATION_ID_CONFIG: app name must be unique in the Kafka
      cluster
    + BOOTSTRAP_SERVERS_CONFIG: where to find Kafka broker(s)

```java
import org.apache.kafka.streams.StreamConfig;
...
final Properties streamConfiguration = new Properties();
streamConfiguration.put(StreamConfig.APPLICATION_ID_CONFIG, "kafka-music-charts");
streamConfiguration.put(StreamConfig.BOOTSTRAP_SERVERS_CONFIG, "broker1:9092,broker2:9092");
streamConfiguration.put(...,...);
```

2) Defining Serdes

Use SERializers and DESerializers (SERDES) to convert bytes of the
record to a specific type

- Keys Serdes can be independent from values Serdes
- There are many build-in Serdes
    + Serdes.String, Serdes.Int, etc.
- JSON for values
- Apache Avro -> custom types

```java
final Map<String, String> serdeConfig = Collections.singletonMap(AbstractKafkaAvroSerDeConfig.SCHEMA_REGISTRY_URL_CONFIG, SCHEMA_REGISTRY_URL);
final SpecificAvroSerde<PlayEvent> playEventSerde = new SpecificAvroSerde<>();
```

3) KStream class

- KStream is a class creates an abstraction over a stream
- Creates a KStream object from one or more Kafka topics

```java
final KStreamBuilder builder = new KStreamBuilder();
final KStream<String, PlayEvent> playEvents = builder.stream(Serdes.String(), playEventSerde, "play-events");
```

4) KTable class

### Transforming Data

#### Stateless Transformation Example

- Filters records based on some specified criteria
- Repartitions based on the new key and value

```java
final KStream<Long, PlayEvent> playsbySongId =
    playEvents.filter((region, event) -> event.getDuration() >= MIN_CHARTABLE_DURATION)     // filtering
              .map((key, value) -> KeyValue.pair(value.getSongId(), value));                // modification
```

Merging Data

- Stream +(Join) Table => enriched stream

```java
final KStream<Long, Song> songPlays = playsBySongId.leftJoin(songTable, (playEvent, song) -> song, Serdes.Long(), playEventSerde);
// leftJoin: join by keys of KStream and KTable; keeping the records in KStream even no key is found in KTable
// first parameter: songTable - a KTable
// second parameter: a lambda
// third parameter: Serdes.Long() - serializer key
// fourth parameter: playEventSerde - serializer objects
```

#### Stateful Processing

![Duality of KStream and KTable](../../graphic/career/jpl/duality-kstream-ktable.png)

### Count (in API)

Example below show a count method

- groupBy: re-partitions the data based a new key
- count: count the number of occurrences of a song, requires the
  application to keep state

Stateful operations can use state stores to store and query data

```java
// groupBy method has three parameters
// first: a lambda describes what we want to group; group by key in this case
// second: type of keys of the new stream
// third: type of values of the new stream
final KGroupedTable<Long, Long> groupedBySongId =
    songPlays.groupBy((songId, song) -> songId, Serdes.Long(), Serdes.Long());

groupedBySongId.count("song-play-count");   // count results are backed by a state store called "song-play-count"
```

### Reduce or Aggregate (custom)

You can combine current record values with previous record values

You may use lambda expressions

In the example below, TopFiveSongs keeps track of the latest top 5 songs
and it is automatically updated as new data comes in

```java
// parameters for aggregate method
// first: the constructor for TopFiveSongs; it creates one instance and passes it along from message to message
// second: a lambda to add things to aggregation
// third: a lambda to take things out of the aggregation
//      the aggKey and value are the key and value of the new element in the stream
//      the aggregate parameter is the instance of the TopFiveSongs object that this aggregate operation is using
// fourth: types
// fifth: name to use for the state store
final KTable<Song, Long> songPlayCounts =
    songPlaysKGroupedTable.aggregate(TopFiveSongs::new,
        (aggKey, value, aggregate) -> { aggregate.add(value); return aggregate; },
        (aggKey, value, aggregate) -> { aggregate.remove(value); return aggregate; },
        topFiveSerde,
        "top-five-songs-by-genre"
    );
```

### Windowing (things come out of aggregation)

Grouping things by time, key

- Actual time (event time) of the events itself (time when it occurs)
  not processing time

![Windowing](../../graphic/career/jpl/windowing.png)

```java
groupedBySongId.count("song-play-count");
groupedBySongId.count(TimeWindows.of(TimeUnit.MINUTES.toMillis(5)), "song-play-count-windowed");
```

## Streams Demo Application

Create a `java.util.Properties` map to specify different Streams
execution configuration values as defined in `StreamConfig`.

- `StreamConfig.BOOTSTRAP_SERVERS_CONFIG`: a list of host/port pairs to
  use for establishing the initial connection to the Kafka cluster
- `StreamsConfig.APPLICATION_ID_CONFIG`: a unique identifier of the
  Streams application to distinguish itself with other applications
  talking to the same Kafka cluster

# Command Line Tools

## Delete a topic

Set `delete.topic.enable=true` in `server.properties`

then you can run this command:

`bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic test`

