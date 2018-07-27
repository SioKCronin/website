---
title: Stream Architecture
menu:
    ai_notes:
        parent: Data Engineering
---

How can you a persistent message queue that scales to millions of messages/second?

For example, today's cars are equipped with a data storage device, the EDR (event
data recorder), which stores all the sensor data for the vehicle. Such data could 
be used for routing, dashboard analytics, or mechanical operation (cruise control, 
lane correction, auto parking, etc). This is just one of many use cases in the IoT 
universe, all requiring connectivity to control centers and real-time processing of data streams.
In many real-world use cases, batch processing does not effectively match reality, 
and real-time processing is required, with a new data maxim, "use it and lose it". 

How do we architect such a system? The answer proposed by Dunning & Friedman's book
**Streaming Arhitecture** is that we use data streams throughout our entire architecture.
We can refer to this as Universal Stream-based Architecture. In this structure data
is used immediately upon ingestion, but still need durability in case processess downstream
aren't ready to process the stream (the data should persist in some way, and be processed
when the stream is flowing again). Another key idea of this architecture is to decouple
data sources from data consumers. Data may flow to an archive, to an aggregator in a 
batch process, and towards stream processing. The point is, each of these consumers
can perform their respective tasks, although their needs from the data are different.
This design is flexible. Features can be added as they emerge in business development, 
without disrupting other existing processes. 

* **producer/publisher**: The data source that sends data to the messaging system.
* **consumer/subscriber**: The processes that use the data provided by the producer.

Here are some essential characteristics we will expect from our messaging system:

* *Fuller independence of the producer and consumer*
* *Persistence* (as mentioned above, we need to be prepared for a hold up in the stream)
* *High rates of messages/second*
* *Naming of topics* (so consumers can subscribe to what they need)
* *A replayable sequence with strong ordering* (useful for picking up the stream and replaying
at any point)
* *Fault tolerance*
* *Geo-distributed replication* (if your service needs to work on all regions, this is required)

Messaging services like Kafka and Map R persist all messages while still handling over 1GB
of message traffic per second per server. 

Distributed system guarentees:
* **at-least-once**: Every record is processed, but some may be processed more than once. 
* **at-most-once**: No record will be processed more than once, but some records may be lost.
* **exactly-once** 

### Apache Storm

* real-time processing of unbounded streams
* represented by Java objects that are constructed as messages are read
* excels as low-latency, real-time analytics
* the first on the scene, so longer history of documentation
* does not support windowing (time period over which aggregations are made in stream processing)

### Apache Spark Streaming

* relies on Resilient Distributed Dataset (RDD), where if jobs are too big for in-memory,
Spark spills to disk
* requires a distributed storage system (like Cassandra)
* works with Java, Python, and Scala

### Apache Flink

* low latency streaming, as well as batch
* treats all batches as a special case of streaming
* like Spark or Storm, requires a distributed storage system

### Kafka transport

* asynchronous, message-based, and persistant
* decouple the producer from the consumer
* require all messages to be acknowledged in order
* sets up oersistence that can last for days or weeks ("surely they're done with that message by now")
* producers send messages to a Kafka broker, which stores and forward messages for many topics
* persistence of messages is unconditional
* offers compaction (retain a message if no later message has been received with the same key), otherwise deleted

### Apache Apex

* both batch and low-latency processing
* runs as a YARN as a application (Yet Another Resource Negotiator --- the resource management layer
of the Hadoop ecosystem)




