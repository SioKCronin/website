---
title: Stochastic Process
menu:
    ai_notes:
        parent: "Math, Probability,& Statistics" 
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
