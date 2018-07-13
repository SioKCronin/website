---
title: Network Geometry
menu:
    ai_notes:
        parent: Math, Probability & Stats
draft: True
---

Network geometry is one of the topics that propelled me towards complexity research
and machine learning. If we accept that interactions between agents in a networked
system have themselves an impact on the dynamics of a system, it follows that we must
investigate the emergence and charactertistics of these interactions. We start to 
wonder how we might reason about these system "overtones".

I find Mulder & Bicaconi's 2018 paper **Network Geometry and Complexity**, which 
introduces their Network Geometry with Flavor framework, to be a nice
primer, so let's start there. First, some terms:

* **simplicial complex** - points, line segements, and triangles (tetrahedrons in 3D, 
and polytope equivalents beyond)
* **cell complex** - formed by gluing convex poltyopes (in this case on the faces 
of the simplicial complexes we'll be evaulating)
* **hyperbolic (Bolyai–Lobachevskian) geometry** - this non-euclidean geometry is used
for saddle surfaces, as we deviate from euclidean space as we hold the postulate that
"for any given line R and point P not on R, in the plane containing both line R and 
point P there are at least two distinct lines through P that do not intersect R."
