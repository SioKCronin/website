---
title: "Space-Time Continuous Models of Swarm Robotic Systems"
menu:
    ai_notes:
        menu: Books
---

Space-Time Continuous Models of Swarm Robotic Systems: Supporting Global-to-Local Programming, 
by Heiko Hamann

## Fundamentals of Swarm Robotics

Multi-robot systems have the ability to show complex behavior, which is one of the features
that motivate my study of them. That, and they have the potential to solve classic problems
in novel, distributed ways. What I'm excited about in this bookis the presentation of how
we derive partial differential equations (Fokker-Planck equation) from a stochastic 
differential equation (Langevin equation), which forms the basis of the Brownian motion model.

To get the party started, Hamann lays out a series of definitions we will return to throughout
this exploration. 

## Brownian motion

Richard Fennman defined Brownian motion as the random motion of particles suspended in a fluid
resulting from their collission with the fast-moving molecules in the fluid. What 
we see are random movements of position for each particle, alternating with displacement 
to new subregions in the space. If the fluid is in thermal equilibrium, then the fluid's
overal linear and angular momenta remain null of over time. You may be asking yourself
what this has to do with robotics, but I think we'll find that the complex behavior
of swarms allows us to conceive of them, at least in one light, as a fluid, and thereby
we can seek to observe some properties already established for fluids (like Bronian motion). 
If that is indeed possible, what would define thermal equilibrium in a robot swarm?

## Modeling swarms

I found this section to be illustrative, in that Hamann shares how different disciplines
have arrived at modeling collective behavior.

### Agent-Based Modeling

This approach is en vogue at the Santa Fe Institute, and has had a long history in 
computer science, stemming back from Nuemann's automata, and, later, Langton's artificial
life. 

### Control Theory

From the author's perspective, there's been work in this space, but the fact that 
the nondeterminism in these models, and how that plays out as coherence breakdowns
stemming from local communication pose a challenge that still needs to be addressed
by this lens.

### Physics

This is where active matter research is revving up. More on that anon.

### Biology

The big breakthroughs, in my opinion, have come from systems biology. This is where
network theory and biology collide. From the author's perspective, the biggest
advances have come from mathematical biology, with the work of Akira Okubo leading the charge. 
Using robot swarms to replicate biological systems has been explored by the author
and Schmickl.
