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

## More than Just a Schema Store

Being out in front of the curve has its advantages, but in tech that can sometimes
mean you are building and maintaining software that will one day be a big fancy
open source project others can plug and play with. Such was the case when Yelp
tackled its schema management. There wasn't a product on the market suited to their 
needs, so they built their own solution, the Schematizer (which is the closest
to a data engineering superhero name I've ever heard). 

In the world of NoSQL databases, schemas can get a bad rap. But as Storm's founder
Nathan Marz puts it, schemas force us to deal with exceptions at the time the data
is added, when the context is the most rich as to what might be wrong, as opposed 
to handling such misisng or incorrectly formatted data downstream, where the context
is the weakest. When used well, schemas can reduce serious debugging headaches
and ensure consumers receive data in the form they expect. 

Yelp uses Avro to represent their schemas, which are defined with JSON. If you're interested
in exploring this landscape, be sure to check out Thrift as well. One of the Avro
features highlighted in this article is schema evolution, which handles what happens
when when Avro schema are changed after data has been written to the data store
using an older version. Here's more [info](https://docs.oracle.com/database/nosql-11.2.2.0/GettingStartedGuide/schemaevolution.html) on schema evolution from Oracle. At Yelp, each
schema that strams through the pipeline is serialized with an Avro schema. The message
itself contains a schema ID, so when it reaches the consumer the consumer can retrieve
the appropriate schema from the Schematizer and deserialize the message. Having 
all the schemas in one place creates a "single point of truth". 

An interesting case worth considering is what happens when an upstream producer
changes the schema of the data it passes to the pipeline. How will this affect 
consumers downstream? This is addressed by the Schematizer, which determines
topics that can safely be assigned to the new schema based on schema compatibility.
This compatibility is determined by Avro resolution roles, which you can read more
about [here](http://avro.apache.org/docs/1.8.0/spec.html#Schema+Resolution). If you
look through the resolution steps, they're pretty intuitive - the schemas have to 
define compatible data structures (i.e. "maps whose value types match", or "have
the same primitive type"). Values from the writer can be "promoted" to what the 
reader expects. For example, **int** is promotable to **long, float** or **double**. 

The primary key fields of the schemas in the Schematizer are used for log compaction,
which is useful for restoring state after a crash. Log compaction retains the last 
update for each key, and a log compacted Kafka topic log contains a full snapshot
of final record values for every record key. Log compaction allows consumers to restore
their state from the log compacted topic. You can learn more about how log compaction works
[here](http://cloudurable.com/blog/kafka-architecture-log-compaction/index.html). 

It's also worth mentioning, that when personally identifiable information (PII) fields
are added to a schema that previously only had non-PII fields, the two schema are 
flagged as incompatible, and the Schematizer creates a new topic for the new schema.
This is great feature for controlling access to private information.

Producers and Consumers are also tracked by the Schematizer. If something needs
attention, this information can be used to contact the appropriate teams. Interestingly,
this data is also available on its own Kafka topic, using [Yelp Kafka](https://github.com/Yelp/yelp_kafka)
which has a host of handy features.
