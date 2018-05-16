---
Title: Hindsight Experience Replay (HER)
menu:
    ai_notes:
        parent: Reinforcement Learning
---

This technique has a super clever way of dealing with sparse reward situations. Essentially, it calls misses successes, so that learning can be made even when we miss our target. It can be combined with other off-policy RL algorithms, and I show how to do that in other posts. 

## Algorithm


```python
algorithm = some_off_policy_RL_algorithm
initialize replay buffer
M = 10 # Number of episodes

for epsisode in range(M):
    goal, s0 = sampler
    for t in range(T):
        
```
