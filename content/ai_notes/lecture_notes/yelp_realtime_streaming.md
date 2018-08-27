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

## Billions of Messages a Day

In 2011, Yelp transitioned to a service oriented architecture (SOA), which scaled
to 150 production services by 2014. Here's a fun factoid shared in the blog. Metcale's 
Law that the effect of a telecommunications network is proportional to the square 
of the number of users connected to the system. This is a shorthand way of characterizing
network effects in complex systems. We can compare this to the services in a SOA.
Ideally we have the effect of all those possible pathways through the system. However, 
if we use RESTFul HTTP connections between all pairs of services this will be difficult
to scale. 

Since 2016, Yelp has had over 100 million reviews, which raises some unique challenges.
"Bulk data applications become service scalability problems". For instance, how would
we handle joins across services? Won't we need to make N service calls for the
**[N+1 Query Problem](https://secure.phabricator.com/book/phabcontrib/article/n_plus_one/)**?

The solution Yelp came up with lies in a message bus and standardized data formatting.
For the bus, Kafka does the heavy lifting, shifting the complexity from $n^2$ to $n$. 
They exploit Kafka's log compaction feature, which prunes topics down, and retains 
only the most recent message for every key. For formatting, they chose Avro, a
space-efficient binary serialization format that integreates nicely with dynamic languages.
What they exploited in their stream architecture was Avro's schema evolution, which
means that reader and writer applications can use different schema versions, provided
they are compatible. This is very cool! Producers can iterate on their schema, without
effecting consumer applications. Schemas are catalogued in an HTTP schema store called 
the "Schematizer", so that data can be transported without schemas. Schemas are retrieved 
and data is decoded at runtime.

So, with a set of Kafka topics regulated by a Schematizer, Yelp's realtime data pipeline
can provide some important guarentees:
* **format** (registered schema are immutable)
* **compatability** (every active schema assigned to a topic is guarenteed
to be compatible with every other active schema assigned to the same topic)
* **registration** (producers and consumers register whenever they produce or consume
data with a schema, so there is a log of which users are using which schema at what
frequency)
* **data ownership** (all schema require documentation, and a team assignment, which
is exposed through an interface called Watson)
* **data availability** (database change capture can reconstruct a complete snapshot)

## Using Services to Break Down Monoliths

I was remarking to a colleague that I've entered the field of data engineering 
at the height of service oriented architecture, and that I actually need to back up 
and learn more about the monoliths from which such systems came. What I've been enjoying
about the Yelp blog is that they share the points of inflection in their systems. 

Here are some of the tools/practices they're using at Yelp to keep their services 
humming (and growing):

* **Swagger** documents the interface of HHTP/JSON services. *swagger-py* will 
automatically create a Python client given a Swagger specification, and *Swagger UI*
provides a centralized directory for all service interfaces.
* **Docker containers** are used to spin up test instances for services, creating 
images that can be pulled in as dependencies by other service authors who wish 
to acceptance test the service.
* **Pyramid** is used as the service stack's web framework, which is a Python
package that "makes it easy to write web applications".
* **gevent** is a coroutine-based Python networking library providing a high-level
synchronous API
* **SmartStack** backs the service discovery system, with each client host running
an HAProxy instance bound to a localhost. A client contacts a service by connecting
to its localhost load balancer which then proxies the request to a service instance.
* **SQLAlchemy** is used as the database access layer.
* **uWSGI** is used behind all the hosting services. 
