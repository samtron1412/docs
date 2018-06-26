[TOC]

# Overview

- Open-source software for reliable, scalable, distributed computing.
- A framework for running applications on large cluster built of
  commodity hardware.
- Four main modules:
    + Hadoop Common: the collection of utilities and libraries that
      support other Hadoop modules
    + **Hadoop Distributed File System** (HDFS - storage part): a
      distributed file system that provides  high-throughput access to
      application data.
    + Hadoop YARN, short for Yet Another Resource Negotiator, is a
      framework for job scheduling and cluster resource management
    + Hadoop **MapReduce** (processing part) is the original processing
      model for Hadoop clusters
        * many other processing models are available for the 2.x version
          of Hadoop
- Related projects:
    + Ambari: a web-based tool for provisioning, managing, and
      monitoring Apache Hadoop clusters
    + Avro: a data serialization system
    + Cassandra: a scalable multi-master database with no single points
      of failure
    + Chukwa: a data collection system for managing large distributed
      systems
    + HBase: a scalable, distributed database that supports structured
      data storage for large tables
    + Hive: a data warehouse infrastructure that provides data
      summarization and ad hoc querying.
    + Mahout: a scalable machine learning and data mining library
    + Pig: a high-level data-flow language and execution framework for
      parallel computation
    + Spark: a fast and general compute engine for Hadoop data
    + Tez: a generalized data-flow programming framework, built on
      Hadoop YARN, which provides  a powerful and flexible engine to
      execute an arbitrary DAGof tasks to process data for both batch
      and interactive use-cases.
    + ZooKeeper: a high-performance coordination service for distributed
      applications

# Installation

- Download: https://hadoop.apache.org/releases.html

# Configuration

- Setting JAVA_HOME in `${HADOOP_HOME}/etc/hadoop/hadoop-env.sh`

# Single Node Setup

## Standalone operation

- By default, Hadoop is configured to run in a non-distributed mode, as
  a single Java process
- The following example copies the unpacked conf directory to use as
  input and then finds and displays every match of the given regular
  expression. Output is written to the given output directory

```example
$ mkdir input
$ cp /etc/hadoop/*.xml input
$ hadoop jar /usr/lib/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.0.0.jar grep input output 'dfs[a-z.]+'
$ cat output/*
```

## Pseudo-Distributed Operation

### Setting up

- Hadoop can be run on a single-node in a pseudo-distributed mode where
  each Hadoop daemon runs in a separate Java process.
- The standard startup and shutdown scripts require that Secure Shell
  (SSH) be set up between nodes in the cluster => make sure you have
  sshd enabled and check that you can connect to localhost without a
  passphrase
- `etc/hadoop/core-site.xml`

```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

- `etc/hadoop/hdfs-site.xml`

```
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

### Execution

- Format a new distributed-filesystem
    + `$ bin/hdfs namenode -format`
- start NameNode daemon and DataNode daemon
    + `$ sbin/start-dfs.sh`
    + the hadoop daemon log output is written to the `${HADOOP_LOG_DIR}`
      directory
- Browse the web interface for the NameNode and the JobTracker
    + NameNode: http://localhost:50070/
- Make the HDFS directories required to execute MapReduce jobs
    + `$ bin/hdfs dfs -mkdir /user`
    + `$ bin/hdfs dfs -mkdir /user/<username>`
- Copy the input files into the distributed filesystem
    + `$ bin/hdfs dfs -put /etc/hadoop input`
- Run some of the examples provided:
    + `$ bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.0.0.jar grep input output 'dfs[a-z.]+'`
- Examine the output files
    + Copy the output files from the distributed filesystem to the local
      filesystem and examine them
        * `$ bin/hdfs dfs -get output output`
        * `$ cat output/*`
    + Or view the output files on the distributed filesystem
        * `$ bin/hdfs dfs -cat output/*`
- When you are done, stop the daemons
    + `$ sbin/stop-dfs.sh`

### YARN on a single node

- You can run a MapRedue job on YARN in a pseudo-distributed mode by
  setting a few parameters and running *ResourceManager* daemon and
  *NodeManger* daemon in addition
- Perform step 1-4 of the above instructions (pseudo-distributed)
- Configure parameters as follows: `etc/hadoop/mapred-site.xml`

```
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```

- `etc/hadoop/yarn-site.xml`

```
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```

- Start ResourceManager daemon and NodeManager daemon
    + `$ sbin/start-yarn.sh`
- Browse the web interface for the ResourceManager
    + ResourceManager: http://localhost:8088/
- Run a MapReduce job
- When you're done, stop the daemons
    + `$ sbin/stop-yarn.sh`

# Cluster Setup

## Installation

- Unpacking the software on all the machines in the cluster or
  installing it via a packaging system as appropriate for your operating
  system.
    + It is important to divide up the hardware into functions
- Typically
    + one machine as the NameNode (master)
    + one machine as the Resource Manager (master)
    + the rest of the machines act as both DataNode and NodeManager
      (workers)

## Configuring Hadoop in Non-Secure Mode

### Introduction

- Two types of important configuration files
    + Read-only default configuration: core-default.xml,
      hdfs-default.xml, yarn-default.xml and mapred-default.xml
    + Site-specific configuration: etc/hadoop/core-site.xml,
      etc/hadoop/hdfs-site.xml, etc/hadoop/yarn-site.xml, and
      etc/hadoop/mapred-site.xml
- control the Hadoop scripts found in the bin/ directory
    + by setting site-specific values via the etc/hadoop/hadoop-env.sh
    + etc/hadoop/yarn-env.sh
- List of all nodes: `etc/hadoop/(slaves/workers)`
- To configure the Hadoop cluster you will need to configure
    + the environment in which the Hadoop daemons execute
    + as well as the configuration parameters for the Hadoop daemons
- Hadoop daemons
    + HDFS daemons
        * NameNode
        * SecondaryNameNode
        * DataNode
    + YARN daemons
        * ResourceManager
        * NodeManager
        * WebAppProxy
    + MapReduce
        * MapReduce Job History Server

### Configuring Environment of Hadoop Daemons

- site-specific customization of the Hadoop daemons' process
  environment:
    + etc/hadoop/hadoop-env.sh
    + optionally, etc/hadoop/mapred-env.sh, and etc/hadoop/yarn-env.sh
- At least, you must specify the JAVA_HOME
    + put the hard link not ${JAVA_HOME}
- You can configure individual daemons using the configuration options
  through environment variables

| Daemon                        | Environment Variables         |
| -                             | -                             |
| NameNode                      | HADOOP_NAMENODE_OPTS          |
| DataNode                      | HADOOP_DATANODE_OPTS          |
| Secondary NameNode            | HADOOP_SECONDARYNAMENODE_OPTS |
| ResourceManager               | YARN_RESOURCEMANAGER_OPTS     |
| NodeManager                   | YARN_NODEMANAGER_OPTS         |
| WebAppProxy                   | YARN_PROXYSERVER_OPTS         |
| Map Reduce Job History Server | HADOOP_JOB_HISTORYSERVER_OPTS |

```bash
# To configure Namenode to use parallelGC, the following statement
# should be added in hadoop-env.sh

export HADOOP_NAMENODE_OPTS="-XX:+UseParallelGC"
```

- Useful configuration parameters
    + HADOOP_PID_DIR: the directory where the daemon's process id files
      are stored
    + HADOOP_LOG_DIR
    + HADOOP_HEAPSIZE / YARN_HEAPSIZE
        * the maximum amount of heapsize to use, in MB
- In most cases, you should specify the HADOOP_PID_DIR and
  HADOOP_LOG_DIR directories such that they can only be written to by
  the users that are going to run the hadoop daemons to avoid the
  potential for a *symlink attack*
- It's traditional to configure HADOOP_PREFIX in the system-wide shell
  environment configuration
    + for example, a script inside /etc/profile.d

```
HADOOP_PREFIX=/path/to/hadoop
export HADOOP_PREFIX
```

### Configuring the Hadoop Daemons

- https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/ClusterSetup.html#Configuring_the_Hadoop_Daemons

- etc/hadoop/core-site.xml

| Parameter           | Value        | Notes                                           |
| -                   | -            | -                                               |
| fs.defaultFS        | NameNode URI | hdfs://host:port/                               |
| io.file.buffer.size | 131072       | size of read/write buffer used in SequenceFiles |

```xml
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
</configuration>
```

- etc/hadoop/hdfs-site.xml
    + NameNode
    + DataNode
- etc/hadoop/yarn-site.xml
    + ResourceManager and NodeManager
    + only ResourceManager
    + only NodeManager
    + History Server
- etc/hadoop/mapred-site.xml
    + MapReduce applications
    + MapReduce JobHistory Server

```xml
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
</configuration>
```


## Monitoring Health of NodeManagers

- Administrators can configure the NodeManager to run an administrator
  supplied script periodically to determine if a node is healthy or not.
    + Administrators can determine if the node is in a healthy state by
      performing any checks of their choice in the script.
    + If the script detects the node to be in an unhealthy state, it
      must print a line to standard output beginning with the string
      ERROR
    + The NodeManager spawns the script periodically and checks its
      output.
        * If the script's output contains the string ERROR, the node's
          status is reported as unhealthy and the node is black-listed
          by the ResourceManager.
        * No further tasks will be assigned to this node
        * However, the NodeManager continues to run the script, so that
          if the node becomes healthy again, it will be removed form the
          blacklisted nodes on the ResourceManager automatically.
- THe following parameters can be used to control the node health
  monitoring script in etc/hadoop/yarn-site.xml

| Parameter                                         | Value                               | Notes                                                |
| -                                                 | -                                   | -                                                    |
| yarn.nodemanager.health-checker.script.path       | Node health script                  | Script to check for node's health status             |
| yarn.nodemanager.health-checker.script.opts       | Node health script options          | Options for script to check for node's health status |
| yarn.nodemanager.health-checker.interval-ms       | Node health script interval         | Time interval for running health script              |
| yarn.nodemanager.health-checker.script.timeout-ms | Node health script timeout interval | Timeout for health script execution                  |

## Workers File

- List all worker hostnames or IP addresses in your
  etc/hadoop/(slaves/workers) file, one per line
- Helper scripts will use the etc/hadoop/(slaves/workers) file to run
  commands on many hosts at once.
- It is not used for any of the Java-based Hadoop configuration.
- In order to use this functionality, ssh trusts (via either
  passphraseless ssh or some other means, such as Kerberos) must be
  established for the accounts used to run Hadoop.

## Hadoop Rack Awareness

- https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/RackAwareness.html
- It is highly recommended configuring rack awareness prior to starting
  HDFS
- Hadoop components are rack-aware
    + For example, HDFS block placement will use rack awareness for
      fault tolerance by placing one block replica on a different rack.
- Hadoop master daemons obtain the rack is of the cluster workers by
  invoking either an external script or java class as specified by
  configuration files
    + output of the script or java class must adhere to the java
      `org.apache.hadoop.net.DNSToSwitchMapping` interface
    + the interface expects a one-to-one correspondence to be maintained
      and the topology information in the format of `myrack/myhost`,
      where `/` is the topology delimiter, `myrack` is the rack
      identifier, and `myhost`is the individual host.
        * Assuming a single /24 subnet per rack, one could use the
          format of `/192.168.100.0/102.168.100.5` as a unique rack-host
          topology mapping
- To use the java class for topology mapping, the class name is
  specified by the `net.topology.node.switch.mapping.impl` parameter in
  the configuration file
    + An example, NetworkTopology.java, is included with the hadoop
      distribution and can be customized by the Hadoop administrator.
    + Using a Java class instead of an external script has a performance
      benefit in that Hadoop doesn't need to fork external process when
      a new worker node registers itself.
- If implementing an external script, it will be specified with the
  `net.topology.script.file.name` parameter in the configuration files.
    + Hadoop will send multiple IP addresses to ARGV when forking the
      topology script.
    + The number of IP addresses sent to the topology script is
      controlled with `net.topology.script.number.args` and defaults to
      100. If the value is 1, a topology script would get forked for
      each IP submitted by DataNodes and/or NodeManagers
    + script example: https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/RackAwareness.html#bash_Example
- If `net.topology.script.file.name` or
  `net.topology.node.switch.mapping.impl` is not set, the rack id
  `/default-rack` is returned for any passed IP address.

## Logging

- Hadoop uses the Apache log4j via the Apache Commons Logging framework
  for logging
- Edit the etc/hadoop/log4j.properties file to customize the Hadoop
  daemons' logging configuration (log-formats and so on)

## Operating the Hadoop Cluster

- HDFS and YARN should run as separate users
    + For example, hdfs and yarn users

### Startup

- Format a new distributed filesystem
    + `bin/hdfs namenode -format <cluster_name>`
- Start the HDFS NameNode:
    + `sbin/hadoop-daemon.sh start namenode`
- Start a HDFS DataNode:
    + `sbin/hadoop-daemons.sh start datanode`
- Start all the HDFS processes
    + `sbin/start-dfs.sh`
- Start the ResourceManager
    + `sbin/yarn-daemon.sh start resourcemanager`
- Start a standalone WebAppProxy server
    + `sbin/yarn-daemon.sh start proxyserver`
- Start a NodeManager
    + `sbin/yarn-daemons.sh start nodemanager`
- Start all the YARN processes
    + `sbin/start-yarn.sh`
- Start the MapReduce JobHistory Server
    + `sbin/mr-jobhistory-daemon.sh start historyserver`

### Shutdown

- stop the HDFS NameNode:
    + `sbin/hadoop-daemon.sh stop namenode`
- stop a HDFS DataNode:
    + `sbin/hadoop-daemons.sh stop datanode`
- stop all the HDFS processes
    + `sbin/stop-dfs.sh`
- stop the ResourceManager
    + `sbin/yarn-daemon.sh stop resourcemanager`
- stop a standalone WebAppProxy server
    + `sbin/yarn-daemon.sh stop proxyserver`
- stop a NodeManager
    + `sbin/yarn-daemons.sh stop nodemanager`
- stop all the YARN processes
    + `sbin/stop-yarn.sh`
- stop the MapReduce JobHistory Server
    + `sbin/mr-jobhistory-daemon.sh stop historyserver`

# Hadoop MapReduce

- Hadoop splits files into large blocks and distributes them across
  nodes in a cluster
- It then transfers *packaged code (jar, etc.)* into nodes to process
  the data in parallel.
- The Reduce phase

# Architecture

## Introduction

- A master node keeps knowledge about the distributed file system, and
  schedules resources allocation. It hosts two daemons
    + NameNode daemon: manages the distributed file system and knows
      where stored data blocks inside the cluster are
    + ResourceManager daemon: manages the YARN jobs and takes care of
      scheduling and executing processes on worker nodes
- Worker nodes: store the actual data and provide processing power to
  run the jobs. They will host two daemons
    + DataNode daemon: manages the actual data physically stored on the
      node
    + NodeManager daemon: manages execution of tasks on the node


# Troubleshooting

## Incompatible cluster IDs

- copy the datanode clusterID
- format the namenode with that ID
    + `bin/hdfs namenode -format -clusterId CID-8bf63244-0510-4db6-a949-8f74b50f2be9`

# References

[wiki]: https://hadoop.apache.org/
[source]: https://github.com/apache/hadoop
