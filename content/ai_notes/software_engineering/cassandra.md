---
title: Cassandra
menu:
    ai_notes:
        parent: Software Engineering
draft: True
---
OK, so Cassandra is so interesting (and its caching buddy Ignite), that it deserves
its own treatement in notes.

Why is this NoSQL, column-family DB so popular amongst distributed systems? We get 
that the data is highly-available (can read from multiple nodes) and eventually consistent,
but how is the data replicated and served?

## Gossip (Viral) protocol


