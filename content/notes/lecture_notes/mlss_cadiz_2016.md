---
title: "MLSS Cadiz 2016"
menu:
    ai_notes:
        parent: Lecture Notes
---

### John Shulman Deep RL

I found these talks to be super straightforward and helpful. A breath of
fresh air. 

#### Part 1

A brief overview of applications, including robotics, inventory
management, resource allocation (queuing), and routing problems
(sequential decision making problem). 

Differentiating between policy optimization and dynamic programming. In
particular, policy optimization including DFO/Evolutionary algorithms
(derivative-free) and Policy Gradients (using gradients, improves with
more parameters. Dynamic programming requires discrete finite states,
and so must be approximated (for instance, approximating function with
neural nets). Actor-critic methods lie at the intersection, as they use
value functions. 

Deep RL is concerned with control and decision making (compared to motor
and frontal cortex - perhaps basal ganglia as well?). "At any time in
the problem you're solving an optimization problem with GD", using
non-linear function approximators that don't make assumptions about the
form of the functions themselves (whether linear or not). 

Markov Decision Processes (MDP) are defined by (S, A, P), with state
space (S), action space (A), and the transition probability distribution
(P(r, s' | s, a), with reward (r) and next state (s') given by current
state (s) and action (a)). One might also define the initial sate
distribution (\mu) or a discount factor (\gamma) that indicates the
degree to which you care less about stuff in the future than the
present. 

One can define define different settings, including episodic, where you
sample an initial state from \mu and proceed until a terminal state
(defined in the state space) is reached. This termination could be good
(ex. taxi reaches its destination), bad, (ex. robot falls over), or can
be defined by a fixed length (episode ends after 1000 cycles). In this
episode setting we aim to maximize reward per episode. 

We can have deterministic policies (functions) or stochastic policies
(probability distribution of action given state), and these are what we
are optimizing. We can also have parameterized policies where we are
optimizing a parameter vector associated with the policy. 

The cross-entropy method is an example of an evolutionary algorithm,
that at every time t is maintaining a distribution over parameter
vectors. It only views the input parameters (\theta) and their reward,
and views the rest of the MDP as a black box. These work, as he said,
"embarrassingly" well (I think because we are embarrassed that simple
works better than complicated?). 

#### Part 2

We want to calculate the gradient, but we don't know f(x), so we'll
gather a lot of samples of x and use them to estimate the gradient. Two
estimation strategies are explored, score function gradient estimator
and importance sampling. This is a valid approach even if f(x) is
discontinuous, so it's very flexible. 


