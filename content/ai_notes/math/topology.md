---
title: Topology
menu:
    ai_notes:
        parent: Math
draft: False 
---
I have wanted to study topology for over two years now, and have finally carved
out time to begin. I had felt called in this direction for several reasons
(ehem, manifolds and network topology), but it wasn't until recently that 
I found words to articulate why I am eager to get topology in my toolkit. 

Essentially, what little I've already learned of topology is already giving me 
fresh scaffolding upon which to grow my understanding of the relationships 
between individuals and groups of all stripes (particles, people, computers, 
planets). What elements are connected? Are those connections maintained as the system changes? 
What are the zones of influence/sharing/exchange? Math can forge new practices
of imagination that you can then bring to bare on questions you feel compelled
to ask.

I realized that if I didn't root my study of topology into some concrete questions
I would start to drift into its vast ocean, and run the risk of never coalescing 
my imagination in something fresh and useful, so I've decided to focus my attention
on how I can apply Topological Data Analysis (TDA) in my work, and use that to
as my true north. 

Preliminary definitions give us the colors we can fingerpaint with, so let's 
check them out. 

## Topological Spaces

If a space walks up to us and claims itself to be topological, we can verify 
whether it is telling us the truth or not by asking these four questions:

* Do you contain the empty set?
* Do you contain all your elements?
* Do you contain subsets of all the intersections of your subsets?
* Do you contain subsets of all the unions of all your subsets?

It's important to note that the elements can be any mathemetical object. Points.
Sets. Topological spaces. Topologies of topologies? Now we're talkin'!

## Neighbourhoods

A math poem is perhaps best to introduce this color.

If $X$ is a topological space and $p$ is a point in $X$, a neighborhood of $p$
is a subset $V$ of $X$ that includes an open set $U$ containing $p$. So, 
$p \in U \subsetneq V$.

## Topological Data Analysis

Topological Data Analysis (TDA) seeks to reveal the complex topological and 
geometrical structures underlying data. One benefit of knowing this structure
is that it can be used to narrow in on the core features "running the show"
in the system, or at least the features playing a structural role. In my mind,
TDA can play a role in EDA and in priming the canvas for other ML models. There
is still a lot of work to be done in connecting the theory with practice,
but I'm excited about the possibilities. 
