---
title: Topological Data Analysis
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

As with much in ML, the system of orientation and measurement we chose plays a 
big role in how we process and make meaning of our data. In TDA, data is typically
treated as a discrete metric space, or a sample from a metric space. Metric spaces
are spaces were distances between all members of the set are defined. My mind jumps
to Euclidean space, but there are metric spaces elliptic and hyperbolic geometries
as well. Metric spaces were named by good 'ol Felix Hausdorff, but first introduced
by Maurice Frechet. And to be more specific, it is the Euclidean distance of Euclidean
n-space that satifies the metric space specs, as does Banach spaces (complete 
normed vector space). 

Equipped with our understanding of metric spaces, we can venture forth to calculate
Hausdorff distances, which tell us how far two subsets of a metric space are from 
each other (the greatest distance from a point in one set to the closest point
in the other set). We can use these distances to gain an understanding the proximity
of different data sets in our metric space, or comparisons between pairs of 
compact metric spaces (which can be accomplished with the Gromov-Hausdorff distance).
Specifically, the Gromov-Hausdorff distance tells us how far two compact metric
spaces are from being isometric, which is to say bijective. But what of this 
compactness I keep referring to? Compactness refers to a subset of Euclidean space
that is both closed (including its limit points) and bounded (having a fixed length
between all its points). 

I got into simplicial complexes inter great detail elsewhere, but suffice it to say
they play an important role in TDA. In the great intro paper Chazal & Michel 2017,
the authors explore how one can go about building simplicial complexes from data. 
In particular, they introduce two complexes, Vietoris-Rips and Cech, and introduce 
the concept of a cover. Formally, a cover of a set X is a collection of sets whose
union contains X as a subset. In this case we say "C covers X". A subcover of C
is a subset of C that covers X, and we deem C an "open cover" if each of its members
is an open set (contained in T, the topology of X). And here's a term whose name I LOVE.
A **refiniement** of C is a cover D of X such that ever set in D is contained 
in some set of C.  

Oh my, you're probably thinking "when will this list of definitions stop", but
I like to think of each concept as an imgination color we can paint with. I promise,
it all comes together in some pretty dazzling fireworks displays. For now, let's 
turn our attention to the **Nerve Theorem**. 
