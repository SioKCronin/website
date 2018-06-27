---
title: Outlier Detection
menu:
    ai_notes:
        parent: Swarm Intelligence
draft: False
---

A paper was brought to my attention today (Particle Swarm Optimization for Outlier Detection) presenting 
a novel application of PSOs in outlier detection, and I wanted to write about it to see 
if I can find my way to some context in operations intelligence (i.e. possibly anomaly detection
in log files?).

As the authors established the outlier problem, I realized that I carry with me a distance 
measurement bias when I think about classifying outliers. The ones far away are from 
the mean are clearly "outliers", right? But of course this depends entirely on what we're
looking for. What are the axes, and what are we interested in finding in the space they define? 
I pressed, I imagine most of us would default to assigning each data point a value 
(distance from the mean, etc.), and then sorting the list to lop off values over some acceptance 
threshold. But, the authors promise, we can do better!

The algorithm uses a distance measurement defined as follows. Suppose we have some field of 
points $P$. Let $p$ be any random point in $P$, and let us establish a circle $O$ with 
origin $p$ and radius $r$. Let $k$ be the number of other points ("neighbors") 
contained by $O$, and assign the value of $k/r$ to $p$. Since we selected $p$ at random,
we can assume now that all points in $P$ now have an associated $k/r$ score. This is where PSO comes in. 
Rather than just guessing what $r$ we need, we can frame the radius settings and the 
observed outcomes as a search space, and send out a swarm of particles to search for optima 
(in this case our $k/r$). The data point with the best value of $r$ that leads to the 
minimum value of the ratio $k/r$ be detected as the top outlier. The particle encoding is 
important for understanding how the algorithm works. Each particle is assigned an ID number, 
and the 3D search space is defined by ($ID$, $r$, $k/r$), so one only needs calculate $k/r$ 
for the points selected by the swarm across the epochs.

The authors observe that in clearly distinguishable subgroupings, where one would 
assume the radius to simply be the one used to define an $r$ that was generated from 
the labeled datasets in training. You know which points should be removed,
so just take the radius setting that excludes them, without false positives from your "include"
group. Yet data in the wild does not cooperate, and makes the setting of $r$ tricky.

Once we've arrived at our optima, one can label neighbors of a certain radius outliers as well.
This could get tricky with "trench-y" data (my unofficial word for what we see being 
tested in the [$Holder table function$](https://en.wikipedia.org/wiki/Test_functions_for_optimization).
Bounds on possible $r$ values are also specified.

I'm going to implement the paper, and will report back on what I find!











