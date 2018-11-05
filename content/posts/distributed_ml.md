---
title: "Strategies and Principles of Distributed ML on Big Data (REVIEW)"
date: "2018-10-5"
---
The central question this paper asks is "how should we distribute our ML programs
over a cluster?". For some of us, the answer is "Spark", and we call it a day.
But if we aren't satisified with the current state of performance, and would like to,
instead, lean into the performance edge between ML models and systems, and explore
the possibilities of improved performance, then we need to dig a little further.

As the authors astutley point out, most ML programs are built to minimize or maximize
a loss function, which means they operationalize an optimization problem. In fact,
the simplification of the global structure of ML programs is one of the strengths of this paper, 
as it helps focus one's attention on the space between models and systems, which 
is the primary aim of their research. The algorithm of choice is applied to create
a series of "iterative-convergent equations" which are repeated until convergence
is reached.

The big takehome of this article is that **dependency structure** and **non-uniform
convergence** of ML programs poses unique challenges in parallel distribution of 
their steps. The principal strategies employed are **data parellism** (dividing
the loss updates over the data points) and **model parallism** (dividing the loss updates
over parts of the model). Data parallelism is a bit more straightforward (think
minibatches), while model parallism requires us to ensure the model parameters 
are truly i.i.d. in their distribution, otherwise we will get different results 
based on which ones we select and in which order.

This leads to four questions, which the authors dive into:

* **How to distribute the computation?**
* **How to bridge computation with inter-machine communication?**
* **How to communicate between machines?**
* **What to communicate?**

