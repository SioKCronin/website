---
title: Processor Scheduling
menu:
    ai_notes:
        parent: Serving Data
draft: False
---

I'm not sure why processor scheduling has so captured my imagination, but I think
because it is so central to computing in general. It's about deciding what happens when. 
It sparks an optimization bubble over my head --- how do we ensure the most efficient scheduling?
The strategy a system employs is called a processor scheduling policy, or discipline.
This discipline will aim to balance processor utilization, throughput, latency, and 
ensuring processes complete before their scheduled deadline. 

At the highest level, **job scheduling** (or **admission scheduling**) determines 
which jobs are even eligible to compete for system resources. The job scheduling policy
determines how many processes can be active in a system at a given time (the 
**degree of multiprocessing**). This policy may create a queue to prevent saturation
of system resources.

The **intermediate-level scheduling** policy determines which processes should
be allowed to compete for processors, and the **low-level scheduling** policy determines
which *ready* processes are assigned to an available processor. We call this low-level
scheduler the dispatcher. 

Before we look at specific algorithms, let's articulate some high-level scheduling objectives:

* *Maximize throughput*
* *Maximize the number of interactive processes receiving acceptable response times*
* *Maximize resource utilization*
* *Avoid indefinite postponement*
* *Enforce priorities* (the queue prioritization)
* *Minimize overhead*
* *Ensure predictability*

In the Deitel brothers operating systems book I culled these from, they highlight that
the several approaches we will explore have the following in common:

* **Fairness**: All like processes are treated similarly. 
* **Predictability**: A particular process should perform the same under similar system loads.
* **Scalability**: Performance should "degrade gracefully" (perhaps the best CS term
I have ever heard), which means we shouldn't see any freezing up, but a gradual decline
in performance as load increases.

On to the scheduling algorithms!

* **FIFO Scheduling**: This is a straightforward queue for processes (seldom used by itself,
although FIFO for processes of the same priority is used).
* **Round Robin Scheduling**: Processes are assigned a quantum, and if they don't complete
their task within that time-limit, they're sent to the end of the ready queue. Often
used as a sub-strategy in a larger master scheme. There's a selfish round robin (SRR)
variant tha favors older processes (using aging; you can tune the priority rates of the 
active and holding queues to control the flow of contenders into the round robin). It is 
worth noting that careful selection of the quantum size q is necessary to maximize the 
benefit of round robin (if it's too long, then you're just back to FIFO). 
* **Shortest-Process-First (SPF) Scheduling**: Uses run-time estimates to select next process.
* **Highest-Response-Ratio-Next Scheduling**: Uses a priority ratio, 
$\frac{time_waiting+service_time}{service_time}$, to determine next process (once priority
hits threshold, it is passed to processor where it is processed to completion). 
* **Shortest-Remaining-Time (SRT) Scheduling**: This is like SPF in that shortest estimated
runtimes are prioritized, but it goes one step further, so if a new process enters the holding
queue that is estimated to be fasters than what remains in the active process, the active 
process gets back to the holding queue and the new fastest is processed. It's a dog 
eat dog world. 
* **Multilevel Feedback Queues**: This is a cool structure of multiple queues. If the
process doesn't complete before the end of the quantum in the top level, it gets bumped
to the next level below. This continues until we get to the end where processes are 
completed round robin.
* **Fair Share Scheduling**: Group processes in some logical way, and then ensure
that each group gets a fair crack at the processors.
* **Deadline Scheduling**: Set specific deadlines for processes. 
