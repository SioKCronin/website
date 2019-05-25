---
title: "A growing neural gas network learns toplogies"
date: "2019-04-14"
---
**A growing neural gas network learns topologies**
by Bernd Fritzke (1995). 

## Overview

Hebbian learning variations for learning topologies in high-dimensional data.

## Key concepts

* **topological learning**: Given some high-dimensional data distributionp, find a topological
structure which closely reflects the topology of the data distribution.

* **competitive Hebbian leanring (CHL)**: For each input signal x connect the two closest centers (measured
by Euclidean distance) by an edge. 

* **vector quantization (VC)**: Often used for data compression, quantization involves dividing a large
set of points (vectors) into groups having approximatley the same number of points closest to them. Each
group is representated by its centroid (similar to k-means). 

* **competitive learning**: A type of ANN where nodes compete for the right to respond to a subset
of input data.

* **neural gas**: For each input signal x adapt the k nearest centers whereby k is
decreasing from a large initial to a small final value. 

