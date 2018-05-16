---
title: K-nearest neighbors
menu:
    ai_notes:
        parent: Software Engineering
---

 Here are four contenders for measuring the nearness of any two points
 in an n-dimensional real vector space with fixed cartesian coordinates:

 ###Euclidean
 As the name suggests, this is the square root of the sum of squares for
 each corresponding input pair of our points. 

 ###Manhattan
 The sum of the lengths of the projections of the line segment between
 the points onto the coordinate axes. Or, how many "city blocks" (i.e.
 coordinate units) lie between the two points. 

 ###Hamming
 The minimum number of substitutions required to change one vector into
 another. Simply tally up how many input position pairs differ.

 ###Minkowski
 This generalizes the Euclidean and Manhattan distance metrics, allowing
 us to to set the sum of distance units (exponent of 1 on differences,
 with 1/1' exponent to norm the sum) or the triangular distance
 (exponent of 2 on differences, with 1/2 exponent to norm the sum). So
 you can toggle between the two to your heart's content. Would we ever
 want higher dimensionality?

 This is all well and good, but what contexts would prompt us to use one
 distance measurement over another? In particular, given the context
 here is particle swarms, which should be used when implementing PSOs?

 This work suggests we consider the dimensionality of our data, and make
 decisions accordingly. Is this being done in practice? There are so
 many parameters to tune with PSOs, is there a straightforward guide to
 making informed decisions for each? Hmm....I feel some sketchnoting
 coming on.
