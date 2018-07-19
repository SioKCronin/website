---
title: Scaling
menu:
    ai_notes:
        parent: Software Engineering
draft: False
---
## Key ideas

* **Vertical scaling**: Throw more power at the problem (faster processors, more cores, more RAM)
* **Horizontal scaling**: Distributed solution.
* **Caching**: Session states need to be stored on an external database or an external
persisten cache, like Redis.
* **Load balancing**: How many load balancers do we need and where should they be positioned
in the topoogy?
* **Database replication**: How are preparing for system failure?
* **Database partitioning**: Can we shunt requests to different branches?
* **Master-Slave replication**: Read from slaves, write to master.
* **Sharding**
* **Denormalization**
