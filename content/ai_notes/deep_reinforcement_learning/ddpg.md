---
title: DDPG
menu: 
    ai_notes:
        parent: Deep Reinforcement Learning
draft: True
---

# Deep Deterministic Policy Gradients (DDPG)

For this model-free RL algorithm for continuous spaces, episodes are generated using a behavioral polcy, which is a noisy version of the target policy. There are two neural networks, an *actor* and a *critic*, where the targets for the critic are the actions outputted by the actor. Actor is trained using mini-batch GD on the inverse expected Q value. 

# Algorithm


```python
algorithm = some_off_policy_RL_algorithm
initialize replay buffer
M = 10 # Number of episodes

for epsisode in range(M):
    
    
```
