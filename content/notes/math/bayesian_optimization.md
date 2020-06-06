---
title: Bayesian Optimization
menu:
    ai_notes:
        parent: Math
draft: True
---

First of all, Katherine Bailey is one of my favorite smart ladies, her explanation
of Gaussian Processes (the flavor of Bayesian optimization I get into there) is 
totally worth the [read](http://katbailey.github.io/post/gaussian-processes-for-dummies/). 
This is a topic that's worth taking the time to build intuition with, as once you have that, 
you can start to see the possibilities of applying Bayesian optimization *everywhere*.

What's nice about Bayesian optimization is that you don't need derivatives. What's 
challenging is selecting your prior and sampling from your posterior distribution. 
What makes the optimization "Bayesian" is that we treat the objective function as an unknown, 
that is, we start with a prior assumption, apply that assumption to our data to generate a 
posterior distribution, and then use the posterior distribution to create a sampling 
function that will give us the next point to sample to gain the most information
about the objective function.

## Gaussian Processes 

In Rassmussen's book two methods are presented - the function approach and the " " approach.
I prefer the function approach, that is to say I see GPs as being this performing inference
on a distribution of functions that can define our observed data. Our goal is not
to arrive at a particular function, but to determine the next best point based on the 
distribution we arrive at.

## Covariance Matrix

If I showed you three points on a 2D plane, and told you would be using a line to
map the relationship of points, how would you determine which two points were closest
to draw a line between? Well, this seems pretty straightforward, but what if we were
looking at the relationship between two points in a 10D space, and are searching
over all the functions we could use to map their relationship? Well, this is where
we can use a covariance matrix to ensure that points close together in our domain
will be considered close when observed in our codomain. 


## Acquisition Functions

### Probability of Improvement

### Expected Improvement

### Upper Confidence Bounds (UCB)

### Thompson Sampling

Choose the action that maximizes the expected reward in regards to a randomly
selected belief. 

