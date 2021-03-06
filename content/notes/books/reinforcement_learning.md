---
Title: "Reinforcement Learning" 
menu:
    ai_notes:
        parent: Books
---

Reinforcement Learning: An Introduction (1998). Richard Sutton & Andrew Barto. 

At the onset, I'm curious to know how much has changed since this book's publication 20 years ago. That being said, as these are two leaders in the field, I'm interested in gaining a sense of their perspective on the history/origin of this subfield, and acclimating to some of the core concepts/constructs. 

### CHAPTER 1
One of the key takeaways from this chapter was the distinction between the value function and rewards function in an RL problem. The value function is ultimately what we are optimizing for, as this is the total cumulative reward, or rather the reward associated with solving the problem at the highest level. The reward function, but contrast, evaluates awards state by state, and can be thought of as the short-term payoff for entering any given state. I like this distinction, because it opens up the idea of scoping the problem, and ensuring you are indeed building a system that achieves what you set out to achieve. That sounds straightforward enough, but given the nuances of building a policy to reinforce even the simplest of goals, the balance of these functions will undoubtedly become a focus of my work. These are the functions we are learning as we build our RL policy. 

There is a treatment of the agent and the environment, as well as a policy and model of the environment. The agent learns while interacting with the environment, which the authors point out is different from evolutionary methods. I'm curious about this distinction, as it is pointed out that genetic algorithms (and perhaps swarm algorithms?) can be used to solve RL problems. I'm putting a map together of how these various approaches relate. 

The distinction between greedy and exploratory moves, and this will come up again in our examination of explore/exploit tradeoffs. This touches upon the balance of reward vs. value function optimization, and also the broader leverage of stochastic process in search problems. The term temporal-difference learning is used, which doesn't seem like much at first blush, but relates in my mind to calculus (derivative, gradient, etc.) - measuring a rate of change between two times (states in these problems).

### CHAPTER 2
n-armed bandit problems are introduced, where the choice to exploit prior knowledge of known advantageous probabilities is pitted against the choice of probabilities that could be advantageous, yet whose probabilities are unknown or more variable. This uncertainty is important. One of the choices with greater variability could in fact be better than the greedy choice in the long-term. How would we make this choice? I'm reminded of simulated annealing. Perhaps policies that take on my risk early on, and then play more conservatively later on?

Incremental implementation involves updating our estimates we go, we we always have an up-to-now vector to reference. 

Nonstationary problem tracking can be addressed with exponential recency-weighted average. The formula presented takes an alpha constant which decays exponentially with (1 - alpha)^k for k time steps. 
Optimistic initial values were introduced as method for encouraging exploration (the agent is continually disappointed with evaluations at each time step, as they are never as good as what was initially observed). 
Reinforcement comparison is raised in the context of an agent not knowing the relative size of a reward (is the reward received average? above average? below?). In this model, preference probabilities are increased by an increment calculated from the difference of the observed reward and the reference reward (often the average of previously received rewards). 
Pursuit methods update preference probabilities of each action so as to increase the likelihood of the greedy option (and decrease the other actions). 
A brief introduction to associative search, in which the n-armed bandit problem is presented in a context where the situation changes play to play, and the agent can learn to associate policies with different situations. 

Interval estimation methods are also introduced, which estimate a confidence interval for the value of each action. The action selected will be the one with the highest upper limit. Bayes optimization is also introduced, with updated posterior probability distributions of action values resulting from any action. I'm curious to see what has grown out of this direction, as posterior probability estimation has seen many recent advances. 

### CHAPTER 3
I keep finding myself circling back to this idea of where we drawing the line between agent and environment. Rather than settling on a specific boundary, can we maintain multiple boundaries at once and allow for these to interact (like we do in multilayer PSO, where each region is the parent region for a system of subregions?). 

The crux of this chapter can be summed up by the Bellman optimality equation for optimal state-value function. When I read through it, I had the same question that this poster on Stack did. I found Sean Easter's answer helpful, and the take home intuition is that we are replacing the general case with what happens in the next time step and all steps after that. I hope to walk through this more slowly with some proofwriting in the coming weeks. I also found this article helpful. 

Beyond that, I found these statements in the summary to be helpful in ... summarizing!

A policy is a stochastic rule by which the agent selects actions as a function of states
The agent's objective is to maximize the amount of reward it receives over time
The discounted formulation is appropriate for continuous tasks (discount rates determine the present value of future rewards)
An environment satisfies the Markov property if its state signal compactly summarizes the past without degrading the ability to predict the future
The Bellman optimality equations are special consistency conditions that the optimal value functions must satisfy
RL adds to Markov Decision Processes a focus on approximation and incomplete information for realistically large problems

### CHAPTER 4
This chapter focusses on Dynamic Programming, and finds its anchor in generalized policy iteration (GPI). With GPI with interleave policy evaluation with policy improvement, which is a common approach for solving RL problems. Policy evaluation involves making the value function consistent with the current policy. Policy improvement involves making the policy greedy with respect to the value function. And then we iterate. 

Another key topic raised in this chapter is policy iteration vs. value iteration. For policy iteration, we use the current policy to find a better policy using V_current_policy, and then calculate V on the new policy to yield a better policy (oh how I wish Squarespace rendered Latex. I know, I know, time to actually build out a better blog). One issue with this approach is that convergence only happens in the limit. 

Value iteration, on the other hand, stops policy iteration after one sweep through the space (all states backed up once). A full backup involves replacing the old policy evaluated at s with the old value of the successor states (their rewards) and the one-step transitions possible under the policy we are evaluating. All possible next steps are backed-up, not just a sample, which is what makes it a full backup. 

"Dynamic programming algorithms are obtained by turning Bellman equations ... into update rules for improving approximations of the desired value functions."

### CHAPTER 5
This chapter dives into Monte Carlo methods for estimating value functions using only sample sequences of states, actions, and rewards. I found it useful to distinguish on-line learning from simulated learning, as this sets the stage for our building. On-line learning requires no prior knowledge of the environment, while simulated learning requires a model to generate sample transitions. Rather than use a model to compute the value of each state, they simply average many returns that start in that state. 

Monte Carlo methods are increment episode by episode (not step by step). Value estimates and policy changes are made at the end of the episode, and it is assume that all episodes terminate no matter what action was taken. The book covers methods that average over complete returns. 

I lost the scent of the book when we hit on-policy and off-policy Monte Carlo, and had to go find some other resources to fill in the gaps. Essentially, off-policy has us applying evaluations from one policy to learn about another, while on-policy has us updating the original policy. 

### CHAPTER 6
At long last, we've arrived at Q-learning (which is where most lectures on Youtube begin). Was it worth the wait? We shall see. 

Temporal difference learning (TD) is introduced as the combination of Monte Carlo and DP, so let's see how this fusion behaves. Differences are explored. Whereas Monte Carlo must wait to the end of the episode to determine the V value (as that is when reward is calculated), TD can make this update in the next time step, using the observed reward and V estimate at t+1. TD updates are sample backups, as they are referencing the value of a successive state to compute a backed-up value, and then using it to change the value of the original state. This differs from the full backups of DP, where we take into
account the complete distribution for all possible successors. 
