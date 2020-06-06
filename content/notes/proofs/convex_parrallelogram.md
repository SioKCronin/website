---
title: Parrallelogram is convex
menu:
    ai_notes:
          parent: Proofs
---

Let $S$ be the parallelogram consisting of all linear combinations of
$t\_{1}v\_{1} + t\_{2}v\_{2}$ with $0 \leq t\_{1} \leq $ and  $0 \leq t\_{2} \leq $,
or equivlently $0 \leq t\_{i} \leq $.

We remember that the line segment $PQ$ consists of all points $(1-t)P +
tQ$ with $0\leq t \leq 1$, and that $PQ$ exists in vector space $S$ if
all points $P, Q$ exist in $S$.

*Proof*. Let $P=t\_{1}v\_{1} + t\_{2}v\_{2}$ and $Q=t\_{1}v\_{1} + t\_{2}v\_{2}$ be points in $S$.

Then

$$(1-t)P + tQ = (1-t)(t\_{1}v\_{1} + t\_{2}v\_{2}) + t(s\_{1}v\_{1} +
s\_{2}v\_{2})$$
$$=(1-t)(t\_{1}v\_{1} + (1-t)(t\_{2}v\_{2}) + t(s\_{1}v\_{1}) +
t(s\_{2}v\_{2})$$
$$=r\_{1}v\_{1} + r\_{2}v\_{2}$$

where $r\_{1} = (1-t)t\_{1} + ts\_{1}$ and $r\_{2} = (1-t)t\_{2} +
ts\_{2}$. 

We have from the exposition that $0 \leq (1-t)t\_{1} + ts\_{1} \leq 1$
and $0 \leq (1-t)t\_{2} + ts\_{2} \leq 1$, so $(1-t)P + tQ =
r\_{1}v\_{1} + r\_{2}v\_{2}$ with $0\leq r\_{i} \leq 1$.

This proves that $(1-t)P + tQ$ is in the paralleogram, which is
therefore convex. $\blacksquare$
