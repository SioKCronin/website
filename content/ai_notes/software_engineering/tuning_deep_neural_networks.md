---
title: Tuning Deep Neural Networks
menu:
     ai_notes:
         parent: Software Engineering
draft: True
---

I first found my way to neural network optimization after getting stuck on a 
Kaggle project. It was a NYC Taxi problem, where you want to predict ride durations
for taxi rides in manhattan. You train on completed rides, and then your test 
input are pick-up locations at specific times of the day, and you are tasked
with predicting how long the trips should be (with performance measured by something
like mean squared difference of predicted durations from actual durations).  

I applied an XGBoost wrapper, and all of a sudden my performance improved. This
was before any feature engineering. This set me on a search for optimizers, and 
I'd like to share that journey here. 

### XGBoost

How does it work and why is it still the gold standard for deep learning optimization?

### HyperOpt



### BayesOpt

There are 

### Optunity


### SwarmOpt

Where are we going with SwarmOpt, and how might we improve upon the projects above?
