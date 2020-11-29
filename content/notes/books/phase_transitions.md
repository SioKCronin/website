---
title: Phase Transitions 
menu:
    ai_notes:
        parent: Books
draft: false
---
by Ricard V. Sole

## Bifurcations and Catastrophes

Let's explore a few key concepts. 

We can study the behavior of complex systems in terms of changes in their
stability. We kick things off with a discussion of bifurcation, which
is a concept attributed to our friend Poincare. Bifurcations are qualitative
changes that occur as we make continous changes to a variable. I like
the example of shifting from vegetation to desert (think Sahara expansion 
in Africa). These clear shifts in the system. 

*Potential functions* are what physicists call harmonic functions in math 
(any real functions with continous second partial derivatives which
satisfy Laplace's equation, which itself desribes situations of equalibrium).

*Symmetry Breaking (SB)* is "a phenomenon in which (infinitesimally) small 
fluctuations acting on a system crossing a critical point decide the system's 
fate." [Wikipedia 11.22.2020]. When there is a continous change to an order
parameter in lockstep with changes in a control parameter, we call such SB
phenomena *second order phase transitions*, but if there is a dramatic shift
over change in a control parameter we call them *catastrophes*. Water to ice
transitions at sea level would be an example. 

*Hysteresis* is the dependence of the state of a system on its history. 

As the critical point is approached, "the characteristic time needed to 
reach the equilibrium state rapidly grows". Noting these changes can give
indication that a critical transition is close at hand. This is one of the 
key reasons I believe phase transitions should be studied - anticipting 
imminent change. 

The author reminds us that in the real world, multiple bifurcations 
cascade around one another, yielding that hard to model thing we call
life. 

## Percolation

What is a system in the first place? What makes something a part of the system
vs. not? This chapter kicks off with this core clarification, concluding 
that a system is a set of items in which there is a path connecting any two 
elements. 

I had never before considered that for something to percolate through a system,
there needs to be a connected path. My mind anchors on the air bubble that
percolates up through a liquid. There is a continuous path that the bubble follows.
We can swap in the example the author gives of the burning forest, with fire
spreading from burning trees to their closest neighbors. For a fire to spread
from one side of the forest to the other there needs to be a connected path
of adjascent trees close enough to catch embers. 

Bethe lattices provide a model of percolation that grants us the ability to
calculate a percolation probability. 
