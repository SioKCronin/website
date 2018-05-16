---
title: "Taking the Human out of the Loop - A Review of Bayesian
Optimization (REVIEW)"
date: "2018-01-16"
---

Taking the Human Out of the Loop: A Review of Bayesian Optimization
(2016). Shahriari et al. Proceedings of the IEEE

### Introduction

* "Mathematically we are considering the problem of finding a global
maximizer (or minimizer) of an unknown objective function f, where X is
some design space of interest; ..."
* "...in global optimization, X is often a compact subset of R^d but the
Bayesian optimization framework can be applied to more unusual search
spaces that involve categorical or conditional inputs."
* "The Bayesian posterior represents our updates beliefs - given data - on
the likely objective function we are optimizing. Equipped with this
probabilistic model, we can sequentially induce acquisition functions
that leverage the uncertainty in the posterior to guide exploration."
* "Intuitively, the acquisition function evaluates the utility of
candidate points for the next evaluation of f; therefore x_n+1 is
selected by maximizing \alpha_n"
