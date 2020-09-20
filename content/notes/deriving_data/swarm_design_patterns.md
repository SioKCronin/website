---
title: Swarm Design Patterns
menu:
    ai_notes:
        parent: Enriching Data
draft: True
---
If you read through a handful of swarm intelligence algorithms, you'll soon 
see some design patterns emerging. I think it is helpful to articulate these
explictly, and wield them as you study more algorithms. 

### Network communication topology

#### Interswarm communication


#### Intraswarm communication
Sometimes we want to apply multiple swarms to different parts of our problem.
This shows up in multiobjective algorithms, as well as single objective problems
conceived of as a collection of parts. If the parts are related, the performance
of one swarm many influence the decisions of others, and thus definingintraswarm 
communication starts to emerge as a topic of interst.  

### Inertia Clamping


### Mutation

Add noise. 


### Velocity Clamping

Sometimes when I implement velocity clamping in particle swarm optimization, I 
find myself wanting to define the functions as the "curb your enthusiasm" suite. 
A particle sees a major possible gain in a particular direction, and decides 
to throw itself whole-heartedly towards it. This is exploitation in its truest 
form. And yet...if we didn't curb such enthusiasm, we'd run the risk of blowing 
past solutions that are even better, thereby diminishing our exploration. 
This wasn't lost on Kennedy and Eberhart, as they followed up their original 
PSO paper with a velocity clamping solution that has since proliferated 
into many variets of clamping (a selection of which I'll outline here). 



