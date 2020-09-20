---
title: Proximal Policy Optimization (PPO)
menu:
    ai_notes:
         parent: Enriching Data
draft: True
---

As I continue spelunking into the PSO cave in hopes of finding an
algorithm design strain of gold I can follow, I'm getting more and more
excited about the RL research at OpenAI. In particular, I perked my ears
up when I read that Proximal Policy Optimzation became the default RL
algorithm at OpenAI last summer. Let's find out why.

First off, what is it PPO?

The stage is set by considering policy gradient methods (PG) in using
deep neural nets in control problems.  Andrej Karpathy has a great
write-up on how these have come about, and I'll write a review of that
separately. The key point is that we stochastically sample actions, and
the actions that happen to lead to good outcomes encourage future such
actions, and likewise future such bad outcomes are discouraged. Like all
stochastic algorithms, results depend on how we proceed through the
space. 
