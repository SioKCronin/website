---
title: Databases
menu:
    ai_notes:
        parent: Software Engineering
draft: False
---
I'd first like to explore the differences between software in the data ecology,
and then dive deeper into key topics affecting their use.

### File System (block storage)
* **HDFS**
* **AWS S3**
* **Azure Blob Storage**
* **Alluxio**
* **Ceph**

### Cache

* **Redis**: OSS in-memory data structure storage, used as a database, cache, and
message broker. Key-value based database system.
* **Memcached**: distributed memory cacheing system. Key-value associative array. 
* **Hazelcast**

### Time Series

* **Apache Cassandra**: Open-source distibuted NoSQL disk database. CQL.
* **Druid**
* **InfluxDB**

### RDMS
* **MySQL**
* **PostgresSQL**

### Geospatial

* **PostgreSQL**
* **Azure Cosmos DB**

### TextSearch

* **ElasticSearch**

### Other

* **Hive**: Data wharehouse built on top of Hadoop. SQL queries must be written in the 
MapReduce Java api.
* **HBase**: Non-relational distributed database written in Java (part of Hadoop), and runs
on top of HDFS.
* **Scribe**
* **MongoDB**
* **DynamoDB**
* **CouchDB**
* **Redshift**
* **Riak**
* **RethinkDB**

## Topics

### Database transaction

A database transaction is a single unit of work that makes a change to a database. 
It can consist of many logical operations. For instances, removing an dollars from 
one bank account and adding them to another could constitute a transaction. 
It has multiple steps, but holds together as a logical unit of work. Database
transactions must be ACID gurenteed, and its an all or nothing situation, meaning
all the operations of the transaction need to happen, or none are applied. 

### Propogation constraints

These ensure changes in one relation do not propogate errors to other relations, 
and include *restricted delete* (can't delete target row until all rows that point to it 
are deleted), *cascades delete* (like restricted delete, only if you delete the 
target row, the rows that point to it will be automatically deleted), and 
*nullifies delete* (you can delete the target value, and all foreign keys pointing
to it are set to null). 

### ACID guarentees

The purpose of ACID (Atomicity, Consistency, Isolation, Durability) is to ensure
data validity even in the event of errors and system failures. What does each guarentee
provide in the face of such faults?

**Atomicity** ensures that all operations/statements of a database transaction execute
fully in order for the unit of work to be considered succesful. If any operations fail,
the entire transaction fails and the database is not changed. So an ACID system ensures
that this happens in any fault event. If there is a power outage halfway through a
transaction, the database will not register the change.

**Consistency** ensures that it is database transactions alone that can bring a
database from one valid state to another. More on that in data integrity.

**Isolation** ensures that concurrent execution of transactions leave the database
in the same state that would have been obtained had the transactions been executed
sequentially.

**Durability** ensures that completed transactions are stored in non-volatile memory.
For instance, if a completed transaction were stored in a cache to later be written
to disk and there was a power outage and the data was loss, that wouldn't be a system
that ensured durability.

I read an interesting Stack post that challenges our assumption that RDBMS are the
only systems that can provide ACID guarentees. NoSQL ACID? Let's see why.

### Data Integrity

Big topic. Fully address it here we can't. Try to summarize we must.

Data should be corrupted while existing in physical storage, and the data itself
should be logical. There's not need storing data that represents an impossible signal
born of faulty hardware or human error. As with many things in life (minus those pesky
network effects that beautifully complexify everything), you get out what you put in.

What's interesting to us as engineers are the contraints we build into our database
systems to ensure data integrity. This includes *entity integrity* (each row in a table
has a non-null unique identifier as its primary key), *referential integrity* (for
a database to be relational, every value of a primary key column of one table 
must have a corresponding value in another attribute in another relation if there
is indeed a relation), and *domain integrity* ensures the domain of values for each
column are defined so that each data will exist in that domain (if it exists at all).

### Rollback

Quite simply, a rollback rolls a database back to some previous state. If something
goes wrong, we want to be able to roll back to a time when things were going right.

### Database trigger

Imagine you run a small company and maintain a relational database to keep track
of all employee data. In your database you have a table for personal information,
with all the security bells and whistles that requires, and then related tables
for teams, payroll, etc. You are onboarding a large number of people, and would like
to create associated records in all tables for each employee, and ensure all those
records are maintained when changes are made to the system. This is a great use
case for a trigger!
