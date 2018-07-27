---
title: Data Engineering Pipeline
menu:
    ai_notes:
        parent: Software Engineering
draft: False
---

### Ingestion

#### File System (block storage of raw data)
* **HDFS**
* **AWS S3**
* **Azure Blob Storage**
* **Alluxio**
* **Ceph**

#### Streaming
* **Kafka**
* **AWS Kinesis**
* **GCP Pub/Sub**
* **Logstash**
* **RabbitMQ**
* **Sqoop**

### Processing
#### Batch Processing
* **AWS lambda**
* **Apache Storm**

#### Unified Processing

* **Flink**

#### Stream Processing

* **Spark Streaming**
* **Storm**
* **Kafka Streams**

### Data Store

#### Cache

* **Redis**: OSS in-memory data structure storage, used as a database, cache, and
message broker. Key-value based database system.
* **Memcached** 
* **Hazelcast**

#### Time Series

* **Apache Cassandra**: Better than Redis on fault tolerance. Has support for HiveQL. Useful
for when you are writing more than reading.
* **Cassandra**
* **Druid**
* **InfluxDB**

#### Geospatial

* **PostgreSQL
* **Azure Cosmos DB

#### TextSearch

* **ElasticSearch**

#### Other

* **Hive**: Data wharehouse built on top of Hadoop. SQL queries must be written in the 
MapReduce Java api.
* **HBase**: Non-relational distributed database written in Java (part of Hadoop), and runs
on top of HDFS.
* **Scribe**
* **MongoDB**
* **DynamoDB**
* **CouchDB**
* **Redshift**

### Web app frameworks

* **Flask**: Web platform for Python

### Orchestrators (workflow management)

* **Airflow**: Author workflows as DAGs.

### Other

* **Ballerina**: [Cloud Native Programming Language](https://ballerina.io/philosophy/)
* **Hadoop**: OSS utilties orchestrating distributed problem solving.
* **Spark**: Unified analytics engine.
* **Capistrano**: OSS framework for building automated deployment scriopts (Ruby).
