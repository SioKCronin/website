---
title: Intersection of Convex Sets
menu:
    ai_notes:
        parent: Proofs
---

Convex sets are interesting in the context of optimization, as they
represent regions where we know we can find global minima. A convex region is a
region where for every pair of points within the region, every point on the line
that joins the points is also within the region.

Fun fact - the intersection of all convex sets containing a given subset A of Euclidean
space, is called the convex hull of A, which is the smallest convex set
containing A. This is the definition needed in the development of Paul
Schatz' Oloid, which can be defined as "the convex hull of a
skeletal frame made by placing two linked congruent circles in
perpendicular planes, so that the center of each circle lies on the edge
of the other circle". More on that anon. 

In the meantime, let's tackle a simple proof to illustrate how the
convex hull develops from the intersection of convex sets.

**Let $S\_{1}$ and $S\_{2}$ be convex sets. Show that $S\_{1} \cap S\_{2}$
is convex.**

*Proof*. Consider any arbitrary point $P \in S\_{1} \cap S\_{2}$.
Without loss of generality, we have from the definition of intersections
that $P \in S\_{1}$, and we know that $S\_{1}$ is a convex set. Since P
was chosen arbitrarily, we have that $S\_{1} \cap S\_{2}$ is also a
convex set. $\blacksquare$

