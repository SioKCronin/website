---
title: Square Root of 2 is Irrational
menu:
   ai_notes:
       parent: Proofs
---

*Proof*. Assume for contradiction that $\sqrt{2}$ is rational.

Therefore, there exists $p, q$ such that $\sqrt{2} = \frac{p}{q}$, where
$q \neq 0$, and $p, q$ share no common divisors other than 1. 

Squaring both sides gives $2 = \frac{p^2}{q^2}$, so consequently $2q^2 =
p^2$.

If a square of a number is even, then the number is even, so there
exists some number $k$ such that $p=2k$. Subsituting this value into the
equation yields $2q^2 = 4k^2$, or $q^2 = 2k^2$.

We see that both $p$ and $k$ have the divisor 2 in common, but this can
not be, so therefore $\sqrt{2}$ is irrational, which is what we needed
to find. $\blacksquare$


