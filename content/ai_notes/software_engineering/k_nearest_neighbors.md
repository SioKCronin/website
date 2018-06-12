---
title: K-nearest neighbors
menu:
    ai_notes:
        parent: Software Engineering
---
Sometimes we want to perform an operation on an agent/vector/particle
based on what we know about its neibhors. Here are contenders for measuring
the nearness of any two points in an n-dimensional real vector space 
with fixed cartesian coordinates, and strategies for using these distances
to calculate neighors:

### Distance

#### Euclidean
As the name suggests, this is the square root of the sum of squares for
each corresponding input pair of our points.

$$d(p,q) = \sqrt{\sum\_{i=1}^n(q\_{i} - p\_{i})^2}$$

#### Manhattan
The sum of the lengths of the projections of the line segment between
the points onto the coordinate axes. Or, how many "city blocks" (i.e.
coordinate units) lie between the two points. 

$$d(p,q) = \sum\_{i=1}^n|q\_{i} - p\_{i}|$$

#### Hamming
The minimum number of substitutions required to change one vector into
another. Simply tally up how many input position pairs differ.

```python
def hamming_distance(s1, s2):
    if len(s1) != len(s2):
        raise ValueError("Undefined for sequences of unequal length")
    return sum(el1 != el2 for el1, el2 in zip(s1, s2))
```

#### Minkowski
This generalizes the Euclidean and Manhattan distance metrics, allowing
us to to set the sum of distance units (exponent of 1 on differences,
with 1/1 exponent to norm the sum) or the "triangular" distance
(exponent of 2 on differences, with 1/2 exponent to norm the sum). So
you can toggle between the two to your heart's content. 

$$D(X,Y) = (\sum\_{i=1}^n|x\_{i} - y\_{i}|^p)^\frac{1}{p}$$

### Neighborhoods

#### Ring Neighborhood

This is typically the neighborhood structure we think of when we think of
"k nearest neighbors". Given a node $x$, return the $k$ (a specified constant)
number of nodes that are the closest to $x$. The "ring" indicated by this name 
can best be visualized if you were to imagine depicting all nodes in the graph 
connected in this way arranged in a ring. 

#### Von Neumann Neighborhood

In a lattice structure, this would be defined as any node and its 
adjascent nodes. This could be extended further to nodes removes by 
some constant $r$. For instance if we are looking for neighbors of 
node $x$ with a $r=2$, then the neighbors would be all nodes who 
have exactly one node seperating them from $x$.
are evaluating. 

