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


# Command Line Tools

## Start Zookeeper

`> bin/zookeeper-server-start.sh config/zookeeper.properties`

## Start Kafka Server

`> bin/kafka-server-start.sh config/server.properties`

## Create a new topic

```bash
> bin/kafka-topics.sh --create \
    --zookeeper localhost:2181 \
    --replication-factor 1 \
    --partitions 1 \
    --topic streams-plaintext-input
```

## List created topics

`> bin/kafka-topics.sh --zookeeper localhost:2181 --describe`

## Start a console producer

`> bin/kafka-console-producer.sh --broker-list localhost:9092 --topic streams-plaintext-input`

## Start a console consumer

```bash
> bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 \
    --topic streams-wordcount-output \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
```

## Delete a topic

Set `delete.topic.enable=true` in `server.properties`

then you can run this command:

`bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic test`


# References

