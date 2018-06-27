[TOC]

# Overview

- 4 supporting libraries
    + Spark SQL
    + Spark Streaming
    + GraphX
    + MLlib
- Resilient Distributed Dataset (RDD)
    + Two types of operations
        * transformations
            - to change the RDD in some way, such as filtering out some
              data
            - RDDs are immutable => the end of result of all
              transformations result in the creation of a new RDD
            - RDDs perform transformations lazily
        * actions
            - use the data contained in the RDDs, and as such when an
              action is called on an RDD, this is when the
              transformations are performed.

# References

[streaming]: https://www.linkedin.com/pulse/spark-streaming-vs-flink-storm-kafka-streams-samza-choose-prakash
[sql]: https://www.dezyre.com/article/spark-sql-vs-apache-drill-war-of-the-sql-on-hadoop-tools/234
