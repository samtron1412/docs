[TOC]

# Overview

Kafka Streams is a client library for processing and analyzing data
stored in Kafka.

# Concepts

- https://docs.confluent.io/4.1.1/streams/concepts.html

## Common

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

## Stream Proccessing Topology

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

## Time

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

## States

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

## Processing Guarantees

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

## Windowing

Windowing controls how to *group records that have the same key* for
stateful operations such as aggregations or joins into so-called
*windows*.

- *Windows* are tracked per record key
- You can specify a *retention period* for the window
    + it controls how long Kafka Streams will wait for *out-of-order* or
      *late-arriving* data records for a given window.
    + in the case of processing time, the semantics are "when the record
      is being processed", which means that the notion of late records
      is not applicable as, by definition, no record can be late.
    + Hence, late-arriving records can only be considered as such for
      event-time or ingestion-time semantics.

# Architecture

- https://docs.confluent.io/4.1.1/streams/architecture.html

## Stream Partitions and Tasks

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

## Threading Model

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

## Local State Stores

The Kafka Streams DSL APIs automatically creates and manages such state
stores when you are calling stateful operators such as `join()` or
`aggregate()`, or when you are windowing a stream

- Every task in Kafka Streams embeds one or more state stores that can
  be accessed via APIs to store and query data required for processing.

## Fault Tolerance

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

# Developer Guide

## Writing a Streams Application

### Libraries and Maven Artifacts

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

### Using Kafka Streams Within Application Code

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

## Configuring a Streams Application

### Steps

1. Create a `java.util.Properties` instance
2. Set the parameters
3. Construct a `StreamsConfig` instance from the `Properties` instance.
   Or you could use `Properties` instance directly

```java
import java.util.Properties;
import org.apache.kafka.streams.StreamsConfig;

Properties settings = new Properties();
// Set a few key parameters
settings.put(StreamsConfig.APPLICATION_ID_CONFIG, "my-first-streams-application");
settings.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, "kafka-broker1:9092");
// Any further settings
settings.put(... , ...);

// Create an instance of StreamsConfig from the Properties instance
StreamsConfig config = new StreamsConfig(settings);
```

### Parameters

- Required
    + application.id
    + bootstrap.servers
- Optional parameters
    + default.deserialization.exception.handler
    + default.production.exception.handler
    + default.key.serde
    + default.value.serde
    + num.standby.replicas
    + num.stream.threads
    + partition.grouper
    + replication.factor
    + state.dir
    + timestamp.extractor
    + ...

## Streams Domain Specific Language (DSL)

The Kafka Streams DSL is built on top of the Streams Processor API.

### Overview

- DSL supports
    + Built-in abstractions for streams and tables: `KStream`, `KTable`,
      and `GlobalKTable`
    + Declarative, functional programming style with stateless
      transformations (e.g. `map` and `filter`) as well as stateful
      transformations such as aggregations (e.g. `count` and `reduce`),
      joins (e.g. `leftJoin`), and windowing (e.g. session windows)
- Define *processor topologies*
    + Specify one or more input streams that are read from Kafka topics
    + Compose transformation
    + Write the resulting output streams back to Kafka topics, or expose
      the processing results of to other applications through
      interactive queries (e.g., via a REST API)

### Creating Sources Streams from Kafka

#### Input Topics (can be multiple topics) -> KStream

- Input topics (record stream) -> KStream (partitioned record stream)

    import org.apache.kafka.common.serialization.Serdes;
    import org.apache.kafka.streams.StreamsBuilder;
    import org.apache.kafka.streams.kstream.KStream;

    StreamsBuilder builder = new StreamsBuilder();

    KStream<String, Long> wordCounts = builder.stream(
        "word-counts-input-topic", /* input topic */
        Consumed.with(
          Serdes.String(), /* key serde */
          Serdes.Long()   /* value serde */
        );

- If you do not specify Serdes explicitly, the default Serdes from the
  configuration are used.
    + You `must specify Serdes explicitly` if the key or value types of
      the records in the Kafka input topics do not match the configured
      default Serdes.

#### Input topic (one topic only) -> KTable

- Reads the specified Kafka input topic into a KTable.
    + the topic is interpreted as a changelog stream, where records with
      the same key are interpreted as UPSERT aka INSERT/UPDATE (when we
      record value is not `null`) or as DELETE (when the value is
      `null`) for that key.
    + You must provide a name for the table (more precisely, for the
      internal *state store* that backs the table)
        * this is required for supporting *interactive queries*
        * when a name is not provided the table will not queryable and
          an internal name will be provided for the state store.
    + Same rules for Serdes as KStream

#### Input topic -> GlobalKTable

```java
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.kstream.GlobalKTable;

StreamsBuilder builder = new StreamsBuilder();

GlobalKTable<String, Long> wordCounts = builder.globalTable(
    "word-counts-input-topic",
    Materialized.<String, Long, KeyValueStore<Bytes, byte[]>>as(
      "word-counts-global-store" /* table/store name */)
      .withKeySerde(Serdes.String()) /* key serde */
      .withValueSerde(Serdes.Long()) /* value serde */
    );
```

### Transform a Stream

#### Stateless transformations

##### Branch: KStream -> KStream[]

- Predicates are evaluated in order
    + a record is placed to one and only one output stream on the first
      match
    + if the nth predicate valuates to true, the record is placed to nth
      stream.
    + If no predicate matches, the record is dropped

```java
KStream<String, Long> stream = ...;
KStream<String, Long>[] branches = stream.branch(
    (key, value) -> key.startsWith("A"), /* first predicate  */
    (key, value) -> key.startsWith("B"), /* second predicate */
    (key, value) -> true                 /* third predicate  */
  );

// KStream branches[0] contains all records whose keys start with "A"
// KStream branches[1] contains all records whose keys start with "B"
// KStream branches[2] contains all other records

// Java 7 example: cf. `filter` for how to create `Predicate` instances
```

##### Filter: KStream -> KStream, KTable -> KTable

Evaluates a boolean function for each element and retains those for
which the function returns true

```java
KStream<String, Long> stream = ...;

// A filter that selects (keeps) only positive numbers
// Java 8+ example, using lambda expressions
KStream<String, Long> onlyPositives = stream.filter((key, value) -> value > 0);

// Java 7 example
KStream<String, Long> onlyPositives = stream.filter(
    new Predicate<String, Long>() {
      @Override
      public boolean test(String key, Long value) {
        return value > 0;
      }
    });
```

##### Inverse Filter

Evaluates a boolean function for each element and drops those for which
the function returns true.

```java
KStream<String, Long> stream = ...;

// An inverse filter that discards any negative numbers or zero
// Java 8+ example, using lambda expressions
KStream<String, Long> onlyPositives = stream.filterNot((key, value) -> value <= 0);

// Java 7 example
KStream<String, Long> onlyPositives = stream.filterNot(
    new Predicate<String, Long>() {
      @Override
      public boolean test(String key, Long value) {
        return value <= 0;
      }
    });
```

##### FlatMap: KStream -> KStream

- Takes one record and produces zero, one, or more records.
    + You can modify the record keys and values, including their types
    + This will mark the stream for data re-partitioning: applying a
      grouping or a join after `flatMap` will result in re-partitioning
      of the records. If possible use `flatMapVlues` instead, which will
      not cause data re-partitioning

```java
KStream<Long, String> stream = ...;
KStream<String, Integer> transformed = stream.flatMap(
     // Here, we generate two output records for each input record.
     // We also change the key and value types.
     // Example: (345L, "Hello") -> ("HELLO", 1000), ("hello", 9000)
    (key, value) -> {
      List<KeyValue<String, Integer>> result = new LinkedList<>();
      result.add(KeyValue.pair(value.toUpperCase(), 1000));
      result.add(KeyValue.pair(value.toLowerCase(), 9000));
      return result;
    }
  );

// Java 7 example: cf. `map` for how to create `KeyValueMapper` instances
```

##### FlatMapValues: KStream -> KStream

```java
// Split a sentence into words.
KStream<byte[], String> sentences = ...;
KStream<byte[], String> words = sentences.flatMapValues(value -> Arrays.asList(value.split("\\s+")));

// Java 7 example: cf. `mapValues` for how to create `ValueMapper` instances
```

##### Foreach: KStream -> void, KTable -> void

- Terminal operation: performs a stateless action on each record
    + Use it to cause side effects based on the input data and then stop
      further processing of the input data
    + Note on processing guarantees: any side effects of an action are
      not trackable by Kafka, which means they will not benefit from
      Kafka's processing guarantees

```java
KStream<String, Long> stream = ...;

// Print the contents of the KStream to the local console.
// Java 8+ example, using lambda expressions
stream.foreach((key, value) -> System.out.println(key + " => " + value));

// Java 7 example
stream.foreach(
    new ForeachAction<String, Long>() {
      @Override
      public void apply(String key, Long value) {
        System.out.println(key + " => " + value);
      }
    });
```

##### GroupByKey: KStream -> KGroupedStream

- Groups the records by the existing key
    + Grouping is a prerequisite for aggregating a stream or a table and
      ensures that data is properly partitioned ("keyed") for subsequent
      operations.
    + Preferable to `groupBy` because it re-partitions data only if the
      stream was already marked for re-partitioning
    + However, `GroupByKey` does not allow you to modify the key or key
      type like `groupBy` does.

```java
KStream<byte[], String> stream = ...;

// Group by the existing key, using the application's configured
// default serdes for keys and values.
KGroupedStream<byte[], String> groupedStream = stream.groupByKey();

// When the key and/or value types do not match the configured
// default serdes, we must explicitly specify serdes.
KGroupedStream<byte[], String> groupedStream = stream.groupByKey(
    Serialized.with(
      Serdes.ByteArray(), /* key */
      Serdes.String())     /* value */
  );
```

##### GroupBy: KStream -> KGroupedStream, KTable -> KGroupedTable

Groups the records by a new key, which may be of a different key type.

- When grouping a table, you may also specify a new value and value type
- `groupBy` is a shorthand of `selectKey(...).groupByKey()`

```java
KStream<byte[], String> stream = ...;
KTable<byte[], String> table = ...;

// Java 8+ examples, using lambda expressions

// Group the stream by a new key and key type
KGroupedStream<String, String> groupedStream = stream.groupBy(
    (key, value) -> value,
    Serialized.with(
      Serdes.String(), /* key (note: type was modified) */
      Serdes.String())  /* value */
  );

// Group the table by a new key and key type, and also modify the value and value type.
KGroupedTable<String, Integer> groupedTable = table.groupBy(
    (key, value) -> KeyValue.pair(value, value.length()),
    Serialized.with(
      Serdes.String(), /* key (note: type was modified) */
      Serdes.Integer()) /* value (note: type was modified) */
  );


// Java 7 examples

// Group the stream by a new key and key type
KGroupedStream<String, String> groupedStream = stream.groupBy(
    new KeyValueMapper<byte[], String, String>>() {
      @Override
      public String apply(byte[] key, String value) {
        return value;
      }
    },
    Serialized.with(
      Serdes.String(), /* key (note: type was modified) */
      Serdes.String())  /* value */
  );

// Group the table by a new key and key type, and also modify the value and value type.
KGroupedTable<String, Integer> groupedTable = table.groupBy(
    new KeyValueMapper<byte[], String, KeyValue<String, Integer>>() {
      @Override
      public KeyValue<String, Integer> apply(byte[] key, String value) {
        return KeyValue.pair(value, value.length());
      }
    },
    Serialized.with(
      Serdes.String(), /* key (note: type was modified) */
      Serdes.Integer()) /* value (note: type was modified) */
  );
```

##### Map: KStream -> KStream

Takes one record and produces one record. You can modify the record key
and value, including their types.

- Applying a grouping or a join after `map` will result in re-
  partitioning of the records. If possible use `mapValues` instead.

```java
KStream<byte[], String> stream = ...;

// Java 8+ example, using lambda expressions
// Note how we change the key and the key type (similar to `selectKey`)
// as well as the value and the value type.
KStream<String, Integer> transformed = stream.map(
    (key, value) -> KeyValue.pair(value.toLowerCase(), value.length()));

// Java 7 example
KStream<String, Integer> transformed = stream.map(
    new KeyValueMapper<byte[], String, KeyValue<String, Integer>>() {
      @Override
      public KeyValue<String, Integer> apply(byte[] key, String value) {
        return new KeyValue<>(value.toLowerCase(), value.length());
      }
    });
```

##### MapValues: KStream -> KStream, KTable -> KTable

```java
KStream<byte[], String> stream = ...;

// Java 8+ example, using lambda expressions
KStream<byte[], String> uppercased = stream.mapValues(value -> value.toUpperCase());

// Java 7 example
KStream<byte[], String> uppercased = stream.mapValues(
    new ValueMapper<String>() {
      @Override
      public String apply(String s) {
        return s.toUpperCase();
      }
    });
```

##### Peek: KStream -> KStream

Performs a stateless action on each record, and returns an unchanged
stream.

- `peek` is helpful for use cases such as logging or tracking metrics or
  for debugging and troubleshooting.

```java
KStream<byte[], String> stream = ...;

// Java 8+ example, using lambda expressions
KStream<byte[], String> unmodifiedStream = stream.peek(
    (key, value) -> System.out.println("key=" + key + ", value=" + value));

// Java 7 example
KStream<byte[], String> unmodifiedStream = stream.peek(
    new ForeachAction<byte[], String>() {
      @Override
      public void apply(byte[] key, String value) {
        System.out.println("key=" + key + ", value=" + value);
      }
    });
```

##### selectKey: KStream -> KStream

Assigns a new key - possibly of a new key type - to each record.

- Calling `selectKey(mapper)` is the same as calling: `map((key, value) -> mapper(key, value), value)`
- Applying a grouping or a join after `selectKey` will result in re-
  partitioning of the records.

```java
KStream<byte[], String> stream = ...;

// Derive a new record key from the record's value.  Note how the key type changes, too.
// Java 8+ example, using lambda expressions
KStream<String, String> rekeyed = stream.selectKey((key, value) -> value.split(" ")[0])

// Java 7 example
KStream<String, String> rekeyed = stream.selectKey(
    new KeyValueMapper<byte[], String, String>() {
      @Override
      public String apply(byte[] key, String value) {
        return value.split(" ")[0];
      }
    });
```

##### Table to Stream: KTable -> KStream

Get the changelog stream of this table

```java
KTable<byte[], String> table = ...;

// Also, a variant of `toStream` exists that allows you
// to select a new key for the resulting stream.
KStream<byte[], String> stream = table.toStream();
```

#### Stateful transformations

##### Overview

Stateful transformations depend on state for processing inputs and
producing outputs and require a state store associated with the stream
processor.

- In aggregating operations, a windowing state store is used to collect
  the latest aggregation results per window.
- In join operations, a windowing state store is used to collect all the
  records received so far within the defined window boundary.
- Available stateful transformations
    + aggregating
    + joining
    + windowing (as part of aggregations and joins)
    + applying custom processors and transformers for Processor API
      integration

![stateful transformation](https://docs.confluent.io/current/_images/streams-stateful_operations.png)

##### Aggregating

After records are grouped by key via `groupByKey` or `groupBy`, and thus
represented as either a `KGroupedStream` or a `KGroupedTable`, they can
be aggregated via an operation such as `reduce`.

- Aggregations are key-based operations, which means that they always
  operate over records (notably record values) of the same key.
- You can perform aggregations on windowed or non-windowed data

> To support fault tolerance and avoid undesirable behavior, the
initializer and aggregator must be stateless. The aggregation results
should be passed in the return value of the initializer and aggregator.
Do not use class member variables because that data can potentially get
lost in case of failure.

---

**Aggregate: KGroupedStream -> KTable, KGroupedTable -> KTable**

- *Rolling aggregation*. Aggregates the values of (non-windowed) records
  by the grouped key. Aggregating is a generalization of `reduce` and
  allows, for example, the aggregate value to have a different type than
  the input values.
- When aggregating a grouped stream, you must provide
    + an initializer (e.g., `aggValue = 0`)
    + an "adder" aggregator (e.g., `aggValue + curValue`)
- when aggregating a grouped table, you must provide
    + a "subtractor" aggregator (`aggValue - oldValue`)

```
KGroupedStream<byte[], String> groupedStream = ...;
KGroupedTable<byte[], String> groupedTable = ...;

// Java 8+ examples, using lambda expressions

// Aggregating a KGroupedStream (note how the value type changes from String to Long)
KTable<byte[], Long> aggregatedStream = groupedStream.aggregate(
    () -> 0L, /* initializer */
    (aggKey, newValue, aggValue) -> aggValue + newValue.length(), /* adder */
    Materialized.as("aggregated-stream-store") /* state store name */
        .withValueSerde(Serdes.Long()); /* serde for aggregate value */

// Aggregating a KGroupedTable (note how the value type changes from String to Long)
KTable<byte[], Long> aggregatedTable = groupedTable.aggregate(
    () -> 0L, /* initializer */
    (aggKey, newValue, aggValue) -> aggValue + newValue.length(), /* adder */
    (aggKey, oldValue, aggValue) -> aggValue - oldValue.length(), /* subtractor */
    Materialized.as("aggregated-table-store") /* state store name */
    .withValueSerde(Serdes.Long()) /* serde for aggregate value */


// Java 7 examples

// Aggregating a KGroupedStream (note how the value type changes from String to Long)
KTable<byte[], Long> aggregatedStream = groupedStream.aggregate(
    new Initializer<Long>() { /* initializer */
      @Override
      public Long apply() {
        return 0L;
      }
    },
    new Aggregator<byte[], String, Long>() { /* adder */
      @Override
      public Long apply(byte[] aggKey, String newValue, Long aggValue) {
        return aggValue + newValue.length();
      }
    },
    Materialized.as("aggregated-stream-store")
        .withValueSerde(Serdes.Long());

// Aggregating a KGroupedTable (note how the value type changes from String to Long)
KTable<byte[], Long> aggregatedTable = groupedTable.aggregate(
    new Initializer<Long>() { /* initializer */
      @Override
      public Long apply() {
        return 0L;
      }
    },
    new Aggregator<byte[], String, Long>() { /* adder */
      @Override
      public Long apply(byte[] aggKey, String newValue, Long aggValue) {
        return aggValue + newValue.length();
      }
    },
    new Aggregator<byte[], String, Long>() { /* subtractor */
      @Override
      public Long apply(byte[] aggKey, String oldValue, Long aggValue) {
        return aggValue - oldValue.length();
      }
    },
    Materialized.as("aggregated-stream-store")
        .withValueSerde(Serdes.Long());
```

- Detail behavior of `KGroupedStream`
    + Input records with `null` keys are ignored
    + When a record key is received for the first time, the initalizer
      is called (and called before the adder)
    + Whenever a record with a non-`null` value is received, the adder
      is called.
- Detail behavior of `KGroupedTable`
    + Input records with `null` keys are ignored
    + When a record key is received for the first time, the initializer
      is called (before the adder and subtractor)
    + When the first non-`null` value is received for a key (e.g.,
      INSERT), then only the adder is called.
    + When subsequent non-`null` values are received for a key (e.g.,
      UPDATE), then (1) the subtractor is called with the old value as
      stored in the table and (2) the adder is called with the new value
      of the input record that was just received. The order of execution
      for the subtractor and adder is not defined.

#### Applying processors and transformers (Processor API integration)

Something

### Writing Streams back to Kafka

Something

## Memory management

- https://docs.confluent.io/4.1.1/streams/developer-guide/memory-mgmt.html

## Tips and Tricks

- Comparing of different datatypes for fast stream
    + http://www.bigendiandata.com/2016-11-15-Data-Types-Compared/

### CastException

- Check SerDes
    + groupBy, groupByKey, to, through
    + Materialized.with(<keySerdes>, <valueSerdes)

# Tutorials

## CEP Streaming Example

- https://github.com/fhussonnois/kafkastreams-cep

## Creating a Streams Application

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

## Transforming Data

### Stateless Transformation Example

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

### Stateful Processing

![Duality of KStream and KTable](../../graphic/career/jpl/duality-kstream-ktable.png)

#### Count (in API)

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

#### Reduce or Aggregate (custom)

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

#### Windowing (things come out of aggregation)

Grouping things by time, key

- Actual time (event time) of the events itself (time when it occurs)
  not processing time

![Windowing](../../graphic/career/jpl/windowing.png)

```java
groupedBySongId.count("song-play-count");
groupedBySongId.count(TimeWindows.of(TimeUnit.MINUTES.toMillis(5)), "song-play-count-windowed");
```

# Streams Demo Application

Create a `java.util.Properties` map to specify different Streams
execution configuration values as defined in `StreamConfig`.

- `StreamConfig.BOOTSTRAP_SERVERS_CONFIG`: a list of host/port pairs to
  use for establishing the initial connection to the Kafka cluster
- `StreamsConfig.APPLICATION_ID_CONFIG`: a unique identifier of the
  Streams application to distinguish itself with other applications
  talking to the same Kafka cluster

# Serialization Frameworks

- http://ganges.usc.edu/pgroupW/images/a/a9/Serializarion_Framework.pdf
- Apache Thrift
- Google Protobuf
- Apache Avro

# Problems

- https://aseigneurin.github.io/2017/08/04/why-kafka-streams-didnt-work-for-us-part-1.html
- https://dzone.com/articles/problems-with-kafka-streams-the-trilogy

# References

[streaming]: https://www.oreilly.com/ideas/the-world-beyond-batch-streaming-101
[flink-vs-streams]: https://www.confluent.io/blog/apache-flink-apache-kafka-streams-comparison-guideline-users/
