---
title: DE stack
menu:
    ai_notes:
        parent: Software Engineering
draft: False
---

### Ingestion

* **Kafka**
* **Sqoop**

### Processing/Buffering
* **AWS lambda**
* **Apache Storm**

### Caching/Storage

* **Memcached**: 
* **Apache Cassandra**: Better than Redis on fault tolerance. Has support for HiveQL. Useful
for when you are writing more than reading.
* **Redis**: OSS in-memory data structure storage, used as a database, cache, and
message broker. Key-value based database system.
* **Hive**
* **HBase**
* **Scribe**
* **MongoDB**
* **DynamoDB**
* **CouchDB**
* **Redshift**

### Viz

* **Flask**

### Other

* **Capistrano**: OSS framework for building automated deployment scriopts (Ruby).
