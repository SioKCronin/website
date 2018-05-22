---
title: Long Short Term Memory (LSTM)
menu:
    ai_notes:
         parent: Reinforcement Learning
---

## Grid Long Short-Term Memory (LSTM)

Long Short-Term Memory (LSTM) networks are networks of LSTM cells
arranged in a grid to facilitate deep and sequential computation. LSTM
networks are RNN architectures with an improved ability to store and
access memory. The magic is a a gating mechansim that controls access to memory cells. The
gating helps preserve signal for longer, and also propogates error for
longer than typical RNN structures. The gating helps focus the network
on specfic aspects of the input signal, while ignoring other parts. An
LSTM network can identify interdenpendencies separated by windows of
time (i.e. identifiable significant connections are not restricted to
adjascent time steps - the *vanishing gradient* problem). 

We will explore the differences between the standard LSTM RNN and the
Stacked and Multidimensional LSTM (referencing the work of Graves et al. 2013). I will then dive into Grid LSTM and what is required for a successful implementation.

Key steps are a *forget gate layer* and *input gate layer*. 

### Standard LSTM

The LSTM network processes a sequence of input-target pairs, generating
an estimated target based on all the input up to that point (which
determines the network's state, which is made up of a hidden vector and
a memory vector). The recurrent weight mastrices are derived (describe
this from Graves 2013). Walk through the gates and h, m.

* $g^{f}$ - forget gate can delete parts of the previous memory vector
($m\_{i-1}$)
* $g^{c}$ - can write new content to the new memory $m\_i$ modulated by
by the input gate $g^{u}$
* $g^{o}$ - this output gates controls what is read from the new memory $m\_{i}$ onto the hidden vector $h$.
* $m'$ - memory vector
* $ h'$ - hidden vector

The memory and hidden vectors define the next state of the network. Each memory vector is obtained by a linear transformation of the
previous memory vector and the gates, so signals are not squashed at
each time step, and backward error signals do not decay sharpy at each
step. Salient signals can be attended to across multiple steps. 

### Stacked LSTM

In a stacked LSTM, the output hidden vector of one LSTM layer is taken
as the input to the next LSTM layer (so sequential stacking).  

### Multidimensional LSTM

Instead of stacking inputs sequentially, an N-dimensional grid is
assembled. This can grow quickly and become unstable in larger grids,
which motivates the need for Grid LSTM. Memory is calculated by summing
up the memory modifications across the N-dimensions. 

### Grid LSTM 

The set-up is similar to multidimensional LSTM, in that there the
network receives input from N hidden vectors and N memory vectors, only
instead of summing them up, the generated output remains separated (so N
h' and N m'). N transforms are are computed (one for each dimension),
which is what yields the output vectors, and each of these transforms
has their own unique weight matrix.


