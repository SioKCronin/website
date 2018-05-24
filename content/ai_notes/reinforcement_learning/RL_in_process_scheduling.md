---
title: RL in Process Scheduling
menu:
    ai_notes:
         parent: Reinforcement Learning
draft: False 
---

When I mentioned my interest in this idea to my partner Carl, he
encouraged me to pursue it, but highlighted that it may be at least a
masters thesis to secure the necessary OS and RL foundations to
implement something that works. I like multi-year challenges, so wanted
to at least start scoping the problem to see what is required. 

At the onset, I think it would be helpful to identify how processes are
currently scheduled (the dominant paradigms), how process scheduling
could be framed as a MDP, and how RL could be applied.

### Overview of Processes and Threads

Processes are the execution of computer programs. They can be made of up
threads that can run one at a time (single-threading) or concurrently (multi-threading), and share memory resources. Multi-threading is what enables parallel execution in multiprocessing systems. This is an exciting area of data engineering for machine learning, as we can reduce computation time for models by optimizing our threading. Multiprocessing will perform differently on different systems, as process scheduling differs between systems, which is why there's potential to move the needle.

### Overview of Process Scheduling

A challenge that emerges is resource vying for shared cache. The
scheduling is decided by a fixed policy, which means the system can not
adapt to dynamic environments, and can not learn from its experiences.
This motivates the need for a self-tuning/optimizing scheduler, and my
goal is to explore how RL could be used in this context. 

### Process scheduling as an MDP

I find that the first key step in applying RL to novel engineering
challenges is effectively setting up the problem as a Markov Decision
Process. Our challenge is formluating the MDP of a thread scheduler.
What are the states in our system? Naim's overview of this topic
suggests some options - average normalized instructions per cycle,
average cache affinity, average cache miss rate. The possible actions
are thread migrations from one core to another, and the reward can be
defined for each state and each core. That seems trick - what would be
our prior on this matrix of rewards? How does learning happen in such a
system?

The goal is to predict the long term rewards of migrating threads on
particular cores. Data is received every scheduling cycle, so it seems
as though a system would have ample data to train. So, who is working on
this and what are the bottlenecks?
