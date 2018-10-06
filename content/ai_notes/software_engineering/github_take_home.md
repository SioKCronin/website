---
title: System design challenge
menu:
    ai_notes:
        parent: Software Engineering
---

## Question 1

**What properties of the CAP theorem would you prioritize for a cloud storage service 
(e.g. Amazon S3, Google Cloud Storage)? What tradeoffs would you have to make?**

I approach the consistency vs. accessibility trade-off as an opportunity to clarify
how our system might best serve our business goals. For example, in systems where 
it is mission-critical that all users see exactly the same records, such as 
systems serving critical care patient medical records, then I would prioritize consistency. 
However, in services where users expect real-time access to information, such as Yelp "closing soon" 
restaurant recommendations, I would prioritize accessibility.

It is wroth mentioning that the the venn diagram often used to depict 
the CAP theorem can sometimes be a bit misleading. The need to 
prioritize either consistency or availability emerges when we partition our data across
servers. You can imagine if you were updating and accessing data from a single database 
on a single server, the conversation of consitency and availability would become
less pressing, as you would assume locking protocols would ensure consistency and
that the availability you had would be what you had. 

## Question 2 
**You are part of a team that is responsible for a large, distributed web application. 
Assume the architecture consists of multiple services running on Kubernetes, using 
primarily MySQL for persistence, and some form of API and user-facing frontend. 
Make whatever other assumptions about the system you wish.**

Let's assume there is a table for users in our MySQL database, and that writes 
are processed by our master nodes and written and replicated to our replicas. Reads
can happen from any node. 

Let's also assume we are using a messaging service like Kafka to coordinate communication
acros our microservices. 

There are many aspects of our system we could explore, but in order to set up 
question 3 well, let's address the following: 

#### Log-in system

Perhaps the most important system design specification we need to understand in order
to address this triage challenge is log-in. Users manually enter their username or password,
or it is populated by a service like 1-Password, or they have a session active in the cache.

The steps of login are, generacially, identify if the user is in the user database
and if their submitted password matches the stored valid password. 

For this challenge, let's assume our login request processing layer receives
a JSON file like this
```
{ timestamp: '1000-01-01 00:00:00', 
  IP: '127.0.0.1/32',
  user: SioKCronin,
  password: IHeartData
}
```

The API might look something like this:

```
SELECT IF( EXISTS(
             SELECT *
             FROM users
             WHERE `user` =  username AND 'password' = password), 1, 0)
```

#### Traffic volume

I'm going to use Yelp's mobile traffic as an example, as their persistence
layer consists of primarily MySQL clusters backed up to Redshift, and they
also orchestrate their deployment of Docker containers with Kubernetes (combined with Mesos
in their in-house system, PaaSTA). 

Yelp sees an average of 32 million unique visitors a month on their mobile app.
If we estimate that 20% of Yelp's users stay logged into the app, these means
there are approximately 26 million users who log in through the app each month.
If we assume the distribution of log ins is constant across the entire day, that 
would mean an average of 10 logins/second. While Yelp is used globally, the lioshare
of its users are in the United States, and they most like have observed hours of peak 
usage, so it would be safe to assume the number of logins per second could excede 
this initial estimate, perhaps extending up to 100s of logins/second, or even 
thousands during peak time. 

The imporant thing to track here is that a large number of users could be negatively 
impacted by log-in latency, especially during peak hours, and similarly, any
rollout of software updates must take into account this steady, high-volume traffic. 

#### Container orchestration

Since we are using Kubernetes, our system is self-healing. If we have nodes down that are not auto-recovering,
this will point us either to our Kubernetes configuration itself or a problem with our cloud host. 
We will not need to investigate individual nodes, except in our cluster logs to see why they failed.

#### Monitoring

Let's assume we are using a monitoring service like Prometheus, so we have realtime data
on how our clusters are doing.

## Question 3

**Users have recently begun complaining of slowness when logging in. Normally 
logins take tens of milliseconds but many users are now seeing logins take 
multiple seconds. Given full access to all the necessary systems, what are 
your initial steps to investigate? Please include what questions you would ask, 
which systems you'd investigate first, which metrics you'd look at, what commands 
you might run, etc. Make sure to explain your reasoning.**

There are three overarching questions I would like to tackle: 

* what happened?
* how can we fix it?
* how can we detect this issue sooner in the future? 

### What happened?

What follows is a cascading list of questions to ask and issues to address, but 
I find it useful to allow one's creativity to at least take a 60 second stab at 
what the major culprits might be. Set a timer, and get the intuitive guesses on
to the table so we can triage from there more dispationately. 

For me these include:

* Perhaps what users are experiencing is isolated, and related to their specific networking environment.
* Perhaps what users are experiencing is browser related, and tied to a recent upgrade.
* Perhaps our database has reached a tipping point that we didn't anticipate in our load testing.
* Perhaps there is another bug we can't quickly identify, and we should rollback our revisions until it is addressed.

This not an exhaustive list, but more like a moment of ventilation to ensure first thoughts
do not vie for attention while a more systematic triage takes place. 

**Which users have been affected?** 

One of the critical pieces of information we have here is that users are successfully
logging in, it is just taking much longer. This rules out a host of directions we 
would need to investigate if users were being denied log-in, or somehow their log-in 
credentials were not accepted in the first place on the front-end (for instance, username
and password input fields not responding).

How many users have reported this issue, and what do they have in common? Geography? 
Similar user names? Similiar log-in times? Android, IOS, desktop)? If similarities 
are encountered, what parts of our system do they point to? Do the similarities relate
to our DB is sharded, thereby possibly indicating a problem in our load balancing or 
in particular nodes in our cluster? Does the regionality of the issue point to possible
issues in our cloud hosting for that region?

**Does our internal testing replicate what the users are experiencing?**

Now that we have cornered the problem. 

Namely, do our tests show what the user is experiencing, and we just overlooked it, 
or does this issue we are triaging exhibit a novel situation we have not covered
with our tests? Can we see a record of this kind of activity in our integration testing?

**What is the state of our clusters?**

Are any nodes down? We have set them up to self-heal, so if they are down, what 
would be preventing them from firing up? One situation might be...

**Has the system experienced any unusual spikes in traffic, and if so, what parts 
of the system do we know this puts pressure on? How are those parts of our system 
responding?**

Can our load balancers serving our client requests handle this traffic? Are our SQL
queries optimized to perform well under such system strain?

**Was something recently deployed that correlates with this phenomena?**

If we have not encountered an obvious error in our clusters or anomalies in 
system traffic that would explain these log-in lags, it is time to evaluate when
did this change begin in order to debug it. Have we recently changed our cache
eviction strategy? This wouldn't explain why we've gone from sub-second latency, to multi-second,
but it is important in our triaging to not assume our issue lies on a single fault line.
Perhaps multiple changes compounded to create the phenomena we are witnessing. 

We can start but running a diff on the container itself

```
Docker diff CONTAINER_ID
```

### How we can we resolve this issue?

This will of course depend on what we discovered above. If we found a bug in the code,
we could manually roll back to a previous version, but we must ask ourselves if restoring 
the previous low latency log-in for these users is more important than the added benefit
of whatever else was included in our last revision (which will be undone if we rollback).
If so, we may choose to live with these low-latencies while we develop a revision
that will solve the problem at hand. Otherwise, it if we choose to rollback, here's
how we might proceed. 

Like 'git reset --hard commitID' in git version control, let's say we want to be 
able to rollback to a specific previous revision in the deployment history.

We can first examine the history to obtain the number,
```
kubectl rollout history deployment/nginx-deployment deployments "nginx-deployment"
```
and rollback to that specific revision.

```python
kubectl rollout undo deployment/nginx-deployment --to-revision=2
deployment.extensions/nginx-deployment
```

This will pull the bug out of production, but doesn't answer our question.

To address whether a table reached a tipping point suspcicion, we will need to... 

### How might we detect such issues sooner going forward? 

The alarming aspect of this problem is that we did not catch it sooner. 
We had to wait until our users complained, which is much too late. 

It is possible our triage inspection will yield the results we are looking for, and the bug
can be fixed in short order. However, it may also be the case that the problem is more 
complex, and will require further troubleshooting. In either case we are going to want
more rigourous test coverage that replicates the conditions that led to the slow 
log-in our users experienced.

Once we feel we have solved the problem and it passes our tests, including load testing, 
then we can set up a canary testing rollout to our nodes. This will requires us to 
set a timeframe under which revisions will be monitored before further rollout takes place. 
We should select time windows that afford the system a chance to monitor the kinds of interaction we expect
from our users. Given the volume we are assuming in this system, we can expect to see
most common activity within a 24 hour timeframe, or perhaps within an hour or minute. 
These rollouts can be timed based on the frequency of the processing they most directly 
address, or if the revision is more broad-reaching, than a typical range of user behaviors
should transpire during the monitoring phase.

And finally, we may find it worthwile to explore what researchers at Twitter have found to 
be successful, which is to train an ML model to predict production success based 
on performance in the testing environment. This layer is to listen to signals that 
aren't detected by our test coverage, but that have historically predicted poor perfmance
in production. 
