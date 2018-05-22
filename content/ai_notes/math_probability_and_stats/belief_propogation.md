---
title: Belief Propogation
menu:
    ai_notes:
         parent: "Math, Probability & Statistics"
---

An approximation algorithm that allows us conduct inference on Bayesian
networks and Markov random fields. Essentially we calculate the marginal
distribution for each unobserved node, given the observed nodes.
Marginal distribution of a given value X is the summation of $p()$ of
all other variables.

Any Bayesian network or Markov random field can be represented as
a factor graph. The algorithm passes real-valued functions, *messages*,
between variables and factors. The messages carry the information of the
influence of the variables on one another. The message differs whether
it is a variable node sending a message to a factor node, or vice versa. The recipient sends as message the constant function equal to 1, the message is the product of all the messages from the neighboring factor nodes. 


