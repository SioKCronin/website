---
title: Yelp Realtime Streaming Data Infrastructure
menu:
    ai_notes:
        parent: Lecture Notes
---

## Fast Order Search Using Yelp's Data Pipeline and Elasticsearch

Yelp was experiencing drag on their food order history page due to database lookups.
Each lookup required a join across four tables. They found they needed both a relational
data store and a key-value store for lantency-sensitive, high-traffic contexts.
They also wanted to support full-text search across their data. After weighing their
options, they chose Elasticsearch.

Deciding on their schema took some planning, as they wanted to prevent the number 
of joins of common operations (that was the situation that led to the change in the first place!).
They sureveyed their clients, and thought about possible future use cases. Yelp persists
MySQL writes to Kafka topics, a topic tracking changes for each table. That provides 
a lot of useful data, but how would we reconstruct high level order updates from those topics?

They explored their data, and saw that high level order changes make changes to their 'Order'
table. 'Order' was a Fact table in their Snowflake schema. This means they could check 
to see if new or updates rows were for existing orders (by checking 'Order'). If they found 
the document was indeed in a finalized state, they could the row's foreign keys to
create a full denormalized order document. 

Let's see how this all comes together with Paastorm, Yelp's in-house stream processor.
An order assembler consumes the Kafka stream of 'Order' updates, references
additional fields from the database, and constructs order documents that can then 
be instered into Elasticsearch. These documents are written to their own Kafka topic,
'assembled_order'. This topic is consumed by Elasticpipe (a connector they built in Flink), 
which writes records out to Elasticsearch. 

What happens if there is divergence between the 'assembled_order'
topic and Elasticsearch? Elasticsearch has a feature called 
[type coercion](https://www.elastic.co/guide/en/elasticsearch/reference/current/coerce.html) that was used.
They developed their own auditing algorithm to ensure Elasticpipe was performing the
way they expected. This algorithm retrieves, sorts, and dedupes all document ids
that should exist in Elasticsearch by scanning the Kafka topic, and then scan Elasticsearch
for possible missing documents using binary search.
