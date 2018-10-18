---
title: Kafka & Kinesis
menu: 
    ai_notes:
        parent: Software Engineering
draft: False
---
In Dunning & Friedman's book **Streaming Architecture**, they state "a big 
difference between stream-based and traditional design ... is that messaging 
layer plays a much more prominent role." 

I am streaming architecture's biggest fan. So many possibilities open up when 
you de-couple producers from consumers, and let your messaging layer do the heavy
lifting on persisting events. To get at some of the finer points
I thought it could be fun to compare the open source project Apache Kafka 
with AWS' pay-to-play Kinesis. Rather than put a firm barrier between the two,
I'd like to move back and forth between them as we build a clearer picture of
streaming architecture in action. But first, some facts about each.

## Kafka

### Language-support & Installation for Kafka

Before we go to far, let's get real about language-support. When I first used Kafka,
I worked with a Python client called [kafka-python](https://github.com/dpkp/kafka-python), 
and there's also Parsely's [pykakfa](https://github.com/Parsely/pykafka), amongst others.
The being said, you will quickly follow the documentation breadcumbs back to their
source, and see that Kafka is written in Scala and Java, and the best documentation
on the block (written by [Confluent](https://www.confluent.io/product/confluent-open-source/))
assumes you are developing in Scala or Java. Even if you plan to work with a Python client,
I encourage you install the Confluent platform so you can follow along with their support
documentation.

### Replay

Replaying a kafka topic from a given offset (the unique identifier of a record 
in a paritition) is one of the great features that shows of Kafka's persistance. 
But how do we do it?

### Kafka Streams

A whole world of opportunities open up with Kafka Stream, as the duality of streams 
and tables (one being able to transform into the other) creates many possibilities 
for creating streams with enriched, processe data. 

## Kinesis

### Terminology

Perhaps the biggest terminology is that Kinesis has **streams**, where Kafka has **topics**.
Kinesis streams can be partitioned into **shards**, and each shared has it's own unique
**partition key**. Shards are composed of **data records**, and each data record is 
composed of a unique **sequence number**, **partition key**, and **data blob**.
