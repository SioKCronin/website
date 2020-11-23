---
title: Networks - an Introduction
menu:
    ai_notes:
        parent: Books
draft: false
---

by M.E.J. Newman

# Chapter 2: Technological Networks

I'm interested in bolstering my understanding of the internet 
as a packet-switching network, and how this compares to other 
networks (circuit-switching, and otherwise). What does network science
have to teach us about network congestion? 

The topic kicks off with a reminder that there is no cartographer
approving new vertices or edges in the network, but rather the
Border Gateway Protocol (BGP) implemented by the world's routers.
I like this quote, "There is no one whose job it is to maintain
an official map of the network". So how do we study the network's 
structure if there's not a map? I have the feeling [traceroute](https://linux.die.net/man/8/traceroute) is involved. 

It appears most internet maps terminate at the router-level. Possible
groupings of router IPs include subnets, domains, and autonomous systems.

# Chapter 18: Dynamical Systems on Networks

The definition of dynamical systems given here suprised me - "any system
whose state, as represented by a some set of quantitative variables, 
changes over time according to some given rules or equations". For some
reason I think I have been conflating the definition of dynamical systems
with complex systems, which the Complex Systems Society defines as - "systems 
where the collective behavior of their parts entails emergence of properties 
that can hardly, if not at all, be inferred from properties of the parts.

One way to begin approaching the analysis of dynamical systems is to study
steady states. We can solve our equation for that point, develop a taylor
series to approximate a polynomial expression of the system, and then 
determine if the fixed point is a attracting or repelling. This is called
linear stability analysis (LSA), and begins with identifying the set of
equilibrium fixed points. You confirm these points by playing out the behavior
of small shifts in intial position. Do these points attract towards a fixed
point, repel from it, or just kind of chill (marginal)? 
