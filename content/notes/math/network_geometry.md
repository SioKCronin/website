---
title: Network Geometry
menu:
    ai_notes:
        parent: Math
draft: false
---

Network geometry is one of the topics that propelled me towards complexity research
and machine learning. If we accept that interactions between agents in a networked
system have themselves an impact on the dynamics of a system, it follows that we must
investigate the emergence and charactertistics of these interactions. We start to 
wonder how we might reason about these system "overtones".

I find Mulder & Bicaconi's 2018 paper **Network Geometry and Complexity** to be a nice
primer, so I'll start there. First, some terms:

* **simplicial complex**: Points, line segements, and triangles (tetrahedrons in 3D, 
and polytope equivalents beyond). In this context these will be used as the building blocks
in our discussion of higher order network structures.
* **cell complex**: These structures are formed by gluing convex poltyopes 
(in this case, affixing them to the faces of the simplicial complexes in our network
based on what "flavor" we've assigned)
* **hyperbolic (Bolyai–Lobachevskian) geometry**: This non-euclidean geometry is used
for saddle surfaces, as we deviate from euclidean space as we hold the postulate that
"for any given line R and point P not on R, in the plane containing both line R and 
point P there are at least two distinct lines through P that do not intersect R."
* **prefential attachment**: This refers to our process of gluing polytopes to our
structure. The process of randomly choosing the face to attach to is sometimes 
referred to as a "stochastic urn process". If this process is linear, than the distribution
of the added components will follow a Yule distribution (with a pmf of $f(k;p)=pB(k,p+1)$). 
* **incidence number**: The number of polytopes glued to the face.
* **generalized degree**: The number of polytopes incident to the face.
* **small-world network**: A small-world network is a type of mathematical graph 
in which most nodes are not neighbors of one another, but the neighbors of any 
given node are likely to be neighbors of each other and most nodes can be reached 
from every other node by a small number of hops or steps
* **superum**: The superum of a subset $S$ of a partially ordered set $T$ is the least
element in $T$ that is greater than or equal to all elements of S, if such an element exists.
* **infimum**: The infimum of a subset $S$ of a partially ordered set $T$ is the greatest
element in $T$ that is less than or equal to all elements of S, if such an element exists.
* **Hausdorff distance**: Measures how far two subsets of a metric space are from each other. 
$\text{d}\_{H}(A,B)$ = $\max\{ \sup\_{a \in A} \inf\_{b \in B} \text{d}(a,b),
\sup\_{b \in B}\inf\_{a \in A}\text{d}(a,b)\}$

### Network Geometry with Flavor (NGF) Evolution

The crux of this model is summed up in the introduction, where it is stated that 
"non-equilibrium growth dictated by purely combinatorial and probabilistic rules
is able to generate an hyperbolic network geometry". The "flavor" in this model 
(which requires all my will to not write as "flavah") refers to specifications for
how the polytopes shall be added (the preferential attachment strategy). This defines
the non-equilbrium development of the network. The authors explore three options, 
but there are infinite variations. 

* **Flavor s=-1**: Attach polytopes only to faces with an existing incidence score of 0.
This will yield a discrete manifold structure, resulting in a Complex Network Manifold.
* **Flavor s=0**: Attach polytopes uniformly across the structure. 
* **Flavor s=1**: Attach polytopes proportional to the generalized degree of the faces. 

### Structures and Dynamics

So we have this network model defined - how do we use it to learn something about the 
network? Well, this has to do with the flavors. With $s=-1$ (the one where we only 
attach to faces with incidence scores of $0$) the NGF is a complex quantum network
manifold (CQNM). The authors explore the thermodynamics of the NGFs (probability of NGF evolution
and total energy of NGF), which starts to hint at how we can work with these models
once they've been generated. Two directions are explored: assessing the emergent
hyperbolic geometry and the manifold topological dimensions.
