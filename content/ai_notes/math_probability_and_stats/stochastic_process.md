---
title: Stochastic Process
menu:
    ai_notes:
        parent: Math, Probability, & Statistics
draft: True
---

One place stochastic process shows up in machine learning is in
optimizing non-convex solutions of systems of equations. If the solution
space is convex and tractable, then there are convex optimization
methods one can use, guarenteeing that any local minima identified will
also be the global minima. However, life often delivers us non-convex
solution spaces.

Applying randomness can help prevent us from artificially limiting the
scope of possible solutions to whatever system we are studying. If an
optimization problem, this means randomness could help us leverage a
more adventurous policy for search.

What role can a random variable play in a mathematical model? How much
randomness is needed to test the resilience of our search, without
knocking us too off course towards convergence to an optimal solution?

### Bernoulli Process

A Bernoulli Process is defined as a sequence of iid Bernoulli random variables,
which are themselves either $0$ or $1$ with probability $p$ and $1-p$ respectively.
They show up in coin tosses, and, well, all over the place actually.

### Wiener Process

I include this in the list, because it is used an exciting phenomena called
the Brownian Motion Process. 

### Markov Chains (random walks)

There are many ways we could define a random walk, but my interests lead me to
Markov Chains, so that is where I situated my understanding. Such processes
satisfy the Markov property, which the conditional probability distribution of 
future states of the process (conditional on both past and present states) 
depends only upon the present state, not on the sequence of events that preceded it.
A Markov Random Field is just this same concept applied to 2+ dimensions.

### Poisson Process
