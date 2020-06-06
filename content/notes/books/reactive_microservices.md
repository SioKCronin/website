---
title: Reactive Microservices Architecture
menu:
    ai_notes:
        parent: Books
draft: False 
---
When my dog Arlo was a puppy, he went through a period where being on a leash
made him anxious, and he would react more agressively to other dogs on the street.
My husband and I took him to a class at the local SPCA called "Reactive Rover"
where he learned to chill out whilst walking on leash. In the context of this
class, reactive was deemed a negative quality we were learning to un-condition, yet, 
in service architecture, reactive takes on an entirely different meaning. 

In software development, it all comes back to the customers, and the teams we 
assemble to serve their needs. I think of nimble teams, iterating to meet the
needs of their customers. Not held back by the system, but supported by its 
ability to test for quality and facilitate deployment. Isolation, and the 
decoupling required to achieve it, is the name of the microservice game, and 
this isolation requires asynchronous communication boundaries between services.

Each service must take sole responsbility for its state and persistence. Services
can ask for the state of other services, but do not have direct access to these 
states. Service persistance can be whatever makes the most sense for that service.
In terms of the **Event Log**, we can either log the commands (**Command Sourcing**)
or the state changes the commands elicit (**Event Sourcing**). This event log
can then be used querying, auditing, replaying, debugging, and replication. I 
like this fresh take on the relationship between the log and the database by
Pat Helland: "The truth is the log. The database is a cache of a subset of the
log. The cached subset happens to be the latest value of each record and index
value from the log."

An important caution is raised, which is that REST is "always at the expense
of decoupling, system evolution, scale, and availability." Whoa! Them be 
fighting words. The point is that REST is most often synchronous, so should 
only be used in contexts of tightly coupled services. RPCs should be investigated
more fully as an alternative, and I will save that for another post. 

A concise history lesson is provided, that shows how we went from storing large
batches in HDFS for large, off-line batch process, to Lambda architecture with
distinct **speed layer** and **batch layer**, which were eventually merged, to
where we are now with "data in motion" extending all the way to the log files 
in each service's data store. 

Another concept that is only touched upon briefly is *Location Transparency*, 
which starts to get at how services will find and communicate with one another
when their code is distributed acorss the cloud cluster. Addressess must be
stable for the life of the service, irregardless of where it is currently being
run. It is also a virtual address, in that it could represent any number of 
instances running the service (as this may scale up and down, depending on 
what is needed).

OK, now to the hit parade of things our microservice architecture should be able
to do.

### Service Discovery

To help services find one another, we can use a pattern called **Inversion
of Control (IoC)**, where each service reports to the platform where it is 
currently running, which can then be made available through a **Service 
Registry** (Client-Side Service Discovery). The locations can also be 
stored in a load balancer (AWS ELB, for instance), or in the address references
themselves (Server-Side Service Discovery). 

### API Management

For services that must communicate with several other services, it is often
preferable to use an API Gateway. This API Gateway will receive the request,
sequence the calls to the necessary APIs (applying protocol translations
where necessary), formatting the responses, and sending the responses back 
to the client. 

### Communication layer

The Enterprise Service Bus (ESB) has traditionally coordinated communication in
Service Oriented Architeture (SOAs), yet systems are evolving to employ
scalable messaging queues (implemented with platforms like Kafka or Kinesis). 
This provides a pub-sub process where producers and consumers can interact 
independently with the queue. It is proposed that pub-sub won't serve all cases
(although I'm curious to hear more compelling edge cases), in which case 
something like Akka Streams, whose actor model abstraction and platform affords
far more control in defining the nuances of a parallel processing/distributed 
system. 

### Integration

How we control the flow of calls/data between systems requires we have some 
protocol defining their interface, and, often, this protocol defines some form
of back-pressure to control the flow of data between the systems. Failures
must also be captured and quarentined to prevent cascading failures. One design
pattern has been to have services emit event streams that other systems can 
consume.
