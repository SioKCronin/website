---
title: Databases
menu: 
    ai_notes:
        parent: Lecture Notes
draft: True
---
Notes from Stanford's online [database](https://lagunita.stanford.edu/courses/DB/2014/SelfPaced/about) 
MOOC.

### Intro

Database Management Systems (DBMS) provide efficient, reliable, convenient and safe
multi-user storage of and access to massive amounts of persistant data. Concurrency 
control can support multi-users. Physical data independence means that data storage on disk
is indpendent of how the program operates on that data. High-level query languages
are declarative (you say what you want, but you don't have to specify the algorithm). 
Efficient systems must ensure the speed and accuracy of 1,000s of queries/second across TBs of data. 

Data models refer to how the data is structured. In relational, this would be a set of records. 
XML captures data as a hierarchical structure of labeled values. Graph data model would
contain nodes and edges.

Schema sets up the structure of the databases, and the data is what is stored (adhering to
that schema). To set up the schema, we can use a data definition language (DDL). 
From there we can start querying and modifying the database using our Data 
Manipulation Language (DML). The database designer would be the one to set up the schema.

The relational model is the foundation of database management systems. Underlies 
all commercial database systems. Tables are sets of named relations. Each column
is a set of named attributes. Instances are the actual data in the table at a given time.
Sets of attributes can be combined to create a unique key. We work with SQL, but
its foundations are in relational algebra.



