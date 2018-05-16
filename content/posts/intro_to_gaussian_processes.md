---
title: "Introduction to Gaussian Processes (REVIEW)"
date: "2018-01-16"
---
Introduction to Gaussian Processes (1998) - David Mackay

### Overview

* "From a  Bayesian perspective, a choice of a neural network model can be
viewed as defining a prior probability distribution over non-linear
functions, and the neural network's learning process can be interpreted
in terms of the posterior probability distribution over the unknown
function. (Some learning algorithms search for the function with maximum
posterior probability, and other Monte Carlo methods draw samples from
this posterior probability)."
* "The idea of Gaussian process modeling is, without parameterizing $y(x)$,
to place a prior $P(y(x))$ directly on the space of functions. The
simplest type of prior over functions is called a Gaussian process. It
can be thought of as the generalization of the Gaussian distribution
over a finite vector space to a function of infinite dimension."
* "Just as a Gaussian distribution is fully specified by its mean and
covariance matrix, a Gaussian process is specified by a mean, often
taken to be the zero function of x, and a covariance function, which
expresses the expected covariance between the value of the function y at
the points x and x'."
* "The actual function y(x) in any one data modeling problem is assumed to
be a single sample from this Gaussian distribution."
* "...by concentrating on the joint probability distribution of the
observed data and the quantities we wish to predict, it is possible to
make predictions with resources that scale as polynomial functions of N,
the number of data points."

* Nonlinear Regression

* In nonparametric methods, predictions are obtained without giving the
unknown function y(x) an explicit parameterization. 
An example of a nonparametric approach to regression is the spline
smoothing method. In this case, the spline priors are Gaussian
processes. 

#### Multilayer Neural Networks and Gaussian Processes

* Neal showed that the properties of a neural network with one hidden
layer converges to those of a Gaussian process as the number of hidden
neurons tends to infinity if the standard 'weight decay' priors are
assumed. 
* The covariance function of this Gaussian process depends on the details
of the priors assumed for the weights in the network and the activation
functions of the hidden units. 

#### Implementation

* DIRECT: "The most obvious implementation fo these equations is to
evaluate the inverse of the covariance matrix exactly. This can be done
using a variety of methods such as Cholesky decomposition, LU
decomposition or Gaussian-Jordan. Having obtained the explicit inverse,
we then apply it directly to the appropriate vectors." 
