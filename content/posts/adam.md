---
title: "ADAM: A Method for Stochastic Optimization (REVIEW)"
date: "2018-01-25"
---

Adam: A Method for Stochastic Optimization (2015). Diederik P. Kingma
and Jimmy Lei Ba. Conference paper at ICLR 2015.

### Overview

* This method computes individual adaptive learning rates for different
parameters from estimates of first and second moments of the gradients.
* Combines AdaGrad (which works well with sparse gradients) and RMSProp
(works well in on-line and non-stationary settings.
