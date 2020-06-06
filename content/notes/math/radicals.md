---
title: Radicals
menu:
    ai_notes:
        parent: Math
draft: False
---

OK, so I have just learned about nested radicals, and want to use them as a 
springboard to meditate on the use of radicals in imagining symmetry in various
dimensions. We begin with the infinite nested radicals problem posed by Srivinas
Ramanujan.

$? = \sqrt{1 + 2\sqrt{1 + 3\sqrt{1 + \dots}}}$.

His solution involves expressing the geometric series under the radical with the 
following general formulation

$? = \sqrt{ax + (n + a)^2 + x\sqrt{a(x+n) + (n+a)^2 + (x+n)\sqrt{\dots}}}$.

To solve the equation on the right, we can set it equal to a function of x, $F(x)$

$F(x) = \sqrt{ax + (n + a)^2 + x\sqrt{a(x+n) + (n+a)^2 + (x+n)\sqrt{\dots}}}$

which we can square and simplify to arrive at

$F(x)^2 = ax + (n + a)^2 + xF(x+n)$.

In the documentation on Wikiepdia there was a leap of faith to the further simplified 
form of 

$F(x) = x + n + a$ 

which I'm still pondering (how do we account for the $F(x + n)$ induction?), but
if we believe that, and set $a=0$, $n=1$, and $x=2$, we can simply equate our nested radicals
with this $x + n + a$, and demonstrate that the nested radicals to infinity equal $3$.
Boom, black box, and all the rest.

For me, the imaginative insight is in expressing the original pattern ($1 + 2\sqrt\dots$) 
as the polynomial $ax + (n+a)^2 xF(x+n)$, and setting $a=0$. It's not obvious
to me how that was conceived, and I'm interested in finding more documentation that
shares the thinking behind this (are there some common paths we can walk to arrive 
at such subsitutions?).

