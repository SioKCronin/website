---
title: Network Geometry
menu:
    ai_notes:
        parent: Math, Probability & Stats
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

### Network Geometry with Flavor

The crux of this model is summed up in the introduction, where it is stated that 
"non-equilibrium growth dictated by purely combinatorial and probabilistic rules
is able to generate an hyperbolic network geometry". The "flavor" in this model 
(which requires all my will to not write as "flavah") refers to specifications for
how the polytopes shall be added (the preferential attachment strategy). The authors
explore three options, but there are infinite variations. 

* **Flavor s=-1**: Attach polytopes only to faces with an existing incidence score of 0.
This will yield a discrete manifold structure, resulting in a Complex Network Manifold.
* **Flavor s=0**: Attach polytopes uniformly across the structure. 
* **Flavor s=1**: Attach polytopes proportional to the generalized degree of the faces. 
