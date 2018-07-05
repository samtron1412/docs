[TOC]

# Overview

# Types

- Event-as-a-time
    + Apache Storm uses this method, which processes each event and uses
      an acknowledgement signal for each.
    + It can impact performance and the cost hardware
- Micro-batching
    + Apache Spark Streaming uses this method, which processes tiny
      groups of events.
    + This method cannot provide a guarantee of in-order processing
- Streaming event window processing
    + windows: markers in the stream (lightweight)
    + non-blocking high performance implementation that can guarantee
      event order and provide only-once, at-least-once, and at-most-once
      event processing with no data loss

# References

[streaming-frameworks]: https://www.quora.com/What-are-the-differences-between-Apache-Spark-Storm-Heron-Samza-Flink-Beam-Apex
