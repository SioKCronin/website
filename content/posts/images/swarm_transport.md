---
title: "Swarm Intelligence systems for transportation engineering:
principles and applications (REVIEW)"
date: "2017-07-13"
---

Dušan Teodorovic. Swarm Intelligence systems for transportation
engineering: principles and applications. Transportation Research, 2008. 

This is one of the most comprehensive articles I have found that
attempts to connect swarm intelligence heuristics to transportation
systems. Most of the article is dedicated to introducing four
multi-agent systems that leverage information sharing models to optimize
search techniques, and I will recap those here. 

Ant Colony Optimization (ACO)

Ants leave pheromone trails, and an ant will use the strength of the
signal to weight their choice of path, as well-trod paths traveled by
ants heading to a food source have a stronger pheromone signal.
Computational applications of this general approach can be observed in
the ant system, ant colony system, and the max-min ant system.  The ant
system has been used to solve the traveling salesman problem (TSP), and
the article includes details on the algorithm. The author also shares
his research on a model that blends ACO with fuzzy logic, which he calls
the Fuzzy Ant System (FAS). This approach takes into account gradations
like visibility and pheromone intensity. FAS seems to give you more
knobs to turn to sensitize your model. The author goes on to spell out
applications of ACO in transportation. 

Particle Swarm Optimization (PSO)

All the birds ("particles") start out flying randomly in search of food.
They keep track of the best fitness value they have achieved thus far
(pbest), while also memorizing the best fitness value of any other
particle (gbest). In each moment, the particles adjust their flying to
take into account pbest and gbest. Two promising transportation examples
are given - PSO in highway incident detection (Srinivasan et al. 2003)
and an application in a vehicle routing problem with time windows (Zhu
et al. 2006). 

Bee Colony Optimization (BCO)

"Bees incrementally add solution components to the current partial
solution and communicate directly to generate feasible solutions". The
artificial bees in this model either fly forward (exploration) or
backward (back to the hive to participate in the decision-making
process). They then go back out to reinforce viable partial paths. 

Stochastic Diffusion Search (SDS)

I'm not sure why the author included this heuristic, since they didn't
present the algorithm or any transportation applications. Maybe four
seemed like a better number than three?
