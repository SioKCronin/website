---
title: Network Topology
menu:
    ai_notes:
        parent: Swarm Intelligence
---

What are the advantages of various topogical structures? How can they be
combined? Mutate over time? How do swarm systems develop communication
topologies?

First, let's get acclimated with the different structures - their
definitions and some useful examples of their use in practice.

[//]: https://networkx.github.io/

![image](shapes.jpg)

### Ring

This is a bus topology in a closed loop, with data traveling around the
ring in one direction, passing through each node in turn until it
arrives where its going. Non-terminal nodes repeat the signal, to give
it a boost. 


### Mesh

Think of a fully connected neural network. If every node in a layer were
also connected to one another, this would be a mesh topology. What we
have instead is a collection of star topologies, wich each node of an
input layer connected to all nodes of the output layer. 

### Star

Everything in a star network passes through the central hub, which
repeats any signal it receives. All works well unless something happens
to this central node.

### Bus

While not necessarily our most efficient, perhaps we can think of the
redundancy as being an asset. Each node is connected to a communication
channel, the bus, with signals eminating from a communicating node in
both directions along the bus. Similar to the star network, this works
fine unless something happens to that central bus. 

### Hierarchical

This structure will feel familiar to what we work with in object orientd
programming - inheritance of information passes from parent to children,
or from children to parents, but not between children or parents. 

