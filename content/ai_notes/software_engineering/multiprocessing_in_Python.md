---
title: Multiprocessing in Python
menu:
    ai_notes:
         parent: Software Engineering
draft: False
---

Multiprocessing opens the door to parallel processing, which can optimize all
sorts of processes, from training deep learning architecture to managing server
requests. Let's see how Python's multiprocessing package works!

## Global Interpreter Lock (GIL)

This is the mechanism that the **CPython** interpreter uses to ensure 
that only one thread excutes Python bytecode at a time. The GIL ensures objects
are safe from concurrent access. The GIL is released during I/O and in some 
computationally-intensive tasks like compression and hashing. 

## Threads

## Process

Process objects represent activity that runs in a separate process, and have
equivalent methods to Threads.

## Pipes and Queues

We can pipe data between processes, or use queues to facilitate multiple producers and consumers.

## Multithreading vs. Multiprocessing

So, in broad strokes, what's the difference between multithreading and multiprocessing?

## multiprocessing

This packages allows us to define a bypass of the GIL to enable local or remote
concurrency. This is done using subprocesses instead of threads. 

Let's establish a motivating example. 

### pool


