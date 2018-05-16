
# Algorithm Design Manual

## 1. Intro to Algo Design

I love the motivation for proof of your algorithm - to confirm that the generalizability of your selected instances (the one's you've tested) holds. 

We then shift into Robot Tour Optimization. Getting to different paths efficiently on the path could be done with a travelling salesman, which requires some stochastic solve. I looked around at how I'd love this, and came back to [neural combinatorial optimization with RL](https://arxiv.org/pdf/1611.09940.pdf). Let's see what the book says!

A jolly romp through algorithms that don't quite cut it: nearest-neighbors, and the vertex one where you find the closests segment that doesn't terminate or close down other segments from happening (closest pair). 

Then we are presented with a scheduling challenge. How can that be solved? I suggest hybrid particle swarms, but was suggested something much more straightforward - optimal scheduling.

This introduction motivates the need for proof-writing. We state what we're trying to prove. Then we list our assumptions we'll use in the proof. Then we establish a chain of reasoning, at the end of which we drop the mic with our little black square. 

We need to make sure our algorithm specifications are clear about the **admissable input** and the required **properties of the output**. We may find the best way forward is to limit input scope down until we have a suitable algorithm. By looking at the definition of classic algorithms, we can start to get a sense of some of these conventions. 

To move an *incorrect* algorithm off the table, one can present a counter-example. To do so you must make sure your counter-example is **verifiable** by showing what answer it produces, and providing a better answer the algorithm failed to find. Thne we make sure the algorithms is in its **simplest form**. We are encouraged to look for counterexamples, and are given some guidance. 

* Think small: when algorithms fail, there is usually a very simple example when they fail.
* Think exhaustively: define cases that cover all possible situations
* Hunt for the weakness, by **going for a tie** or **seeking extremes**

A brief tour of induction, and it's relation to recurssion in computer science, is offered. Errors in induction can creep in under **boundary conditions** and **extension examples** where we think adding one more element doesn't change anything, but in fact shifts the solution. 

Another brief tour of summation, and how it shows up in algorithm analysis. 


```python

```
