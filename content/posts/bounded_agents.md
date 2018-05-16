---
title: Learning the Preference of Bounded Agents (REVIEW)
date: 2017-03-17
---

This paper applies models of bounded and biased cognition to the
creation of a generative model for human choices in decision problems.
Perhaps more importantly, the authors attempt to infer preferences (not
beliefs) from this model.

They focus their attention on four types of agents:

* Hyperbolic-discounting (i.e. my favorite new way of saying
procrastinating)
* Agents using Monte Carlo approximations of expected utility
* "Myopic" agents
* Bounded value-of-information agents

Choice is made in proportion to a softmax function of expected utility:

![softmax](/images/softmax.jpg)

Which relates to simulation of future internal states and choices, where
U is how the agent computes immediate utility, M is how it predicts its
future internal states, and h is how it modifies its state when it is
passed to the choice function.

![future internal](/images/future_internal_state.jpg)
