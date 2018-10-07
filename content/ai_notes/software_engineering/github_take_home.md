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
the CAP theorem can sometimes be a bit misleading when it comes to vetting distributed solutions.
The need to prioritize either consistency or availability emerges when we partition our data across
servers. You can imagine if you were updating and accessing data from a single database 
on a single server, the conversation of consitency and availability would become
less pressing, as you would assume locking protocols would ensure consistency and
that the availability you had would be what you had. 

I find Martin Klepperman's writing in this area to be particularly illuminating. 


Estimating query plans - DB caches the query plans
But there may be moments when the structure of the DB changes, and there needs 
to be a new query plan 



## Question 2 
**You are part of a team that is responsible for a large, distributed web application. 
Assume the architecture consists of multiple services running on Kubernetes, using 
primarily MySQL for persistence, and some form of API and user-facing frontend. 
Make whatever other assumptions about the system you wish.**

Frontend with load balancers.

We will use CDN cacheing for all commonly requested content, with Least Recently Used (LRU) eviction strategy. 

Our data model will be a MySQL table for user information and tables for all the other
amazing things our system does. Writes in our datbase cluster will be processed by our 
master nodes and written and replicated to our replicas. Reads can happen from any node. 
MySQL Workbench will be set up for DB monitoring. We will enable our slow-log by 
setting the appropriate paramters in our $my.cng$ file. Our user table will be indexed
to ensure speedy lookup during log-in verification.

We will use Docker as our container service and Kubernetes 

Depending on what our service does, there are many aspects of our system we could explore, 
but in order to set up question 3 well, let's address the following: 

#### Log-in system

Perhaps the most important system design specification we need to understand in order
to address our triage challenge in Q3 is log-in. Users manually enter their username or password,
or it is populated by a service like 1-Password, or they have a session active in the cache.

The steps of login are, generacially, if the user is in the user database
and if the hash of their submitted password matches the stored value of their 
hashed password, then they are validated and a session is created. For the hashing
we would use some form of cryptographic hashing function (i.e. Argon2), that is deterministic,
quick to compute, and infeasible to generate the original password from the hash.
This hashed password is what will be stored in our user table, and compared
against the hash of the password used at login.

So, we can assume our login request processing layer receives a JSON file like this
```
{ timestamp: '1000-01-01 00:00:00', 
  IP: '127.0.0.1/32',
  user: SioKCronin,
  password: IHeartData
}
```

If we were working with a single local MySQL instance, the API might look something like:

```
import argon2
import mysql.connector

user, password = RETRIEVE FROM SERVER CALL QUEUE

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  passwd="yourpassword",
  database="mydatabase"
)

password = argon2.argon2_hash("IHeartData")

mycursor = mydb.cursor()

mycursor.execute("SELECT *
                  FROM users
                  WHERE `user` =  {} 
                  AND 'hashed_password' = {},
                  LIMIT = 1), 1, 0)".format(user, password)
                )

myresult = mycursor.fetchall()

if myresult:
    pass
    ```
    Validate and initialize session
    ```
else:
    pass
    ```
    Raise error
    ```
```

#### Traffic volume

I'm going to use Yelp's mobile traffic as an example, as their persistence
layer consists of primarily MySQL clusters backed up to Redshift, and they
also orchestrate their deployment of Docker containers with Kubernetes (combined with Mesos
in their in-house system, PaaSTA). 

Yelp sees an average of 100 million unique mobile users a month. If we estimate 
that 20% of Yelp's users stay logged into the app, these means
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

#### Cloud Hosting and Monitoring

Let's assume we are using AWS, with a monitoring service like Prometheus for our cluster maintenance. 
We will set up a VPN with security groups based on the product ownership areas and 
restrictions of our team. 

## Question 3

**Users have recently begun complaining of slowness when logging in. Normally 
logins take tens of milliseconds but many users are now seeing logins take 
multiple seconds. Given full access to all the necessary systems, what are 
your initial steps to investigate?** 

There are three overarching questions I would like to tackle: 

* what happened?
* how can we fix it?
* how can we detect it sooner in the future? 

### What happened?

Before diving in, here are three possibilities I want to make sure are at least
considered, given they were what my gut came up with first (and I find it useful 
to capture intuitive respones at the onset of a triage session):

* has something changed in our code relating to how we process log-in?
* has a table in DB reached a tipping point?
* is a malicious user exploiting some aspect of our system, thereby slowing down login for other users? 

**Which users have been affected?** 

It is imortant to note that so far users are reporting they are successfully
logging in, it is just taking much longer. 

How many users have reported this issue, and what do they have in common? Geography? 
Similar user names? Similiar log-in times? Android, IOS, desktop)? If similarities 
are encountered, what parts of our system do they point to? Do the similarities relate
to our DB is sharded, thereby possibly indicating a problem in our load balancing or 
in particular nodes in our cluster? Does the regionality of the issue point to possible
issues in our cloud hosting for that region?

To start investigating, we'll want to look at the slow-log we enabled for our MySQL cluster. 

```python
mysqldumpslow
```

This will give us a view of all recent slow queries, which, depending on the scope of the problem,
will most likely needed to be filtered further. We can do so by adding a few more flags,
such as **-i** for specific instances (if we identified any) or return only a select number **-t**.

We can also tag on an $EXPLAIN$ to our query, and run it in our dev environment to 
check out our query plan. This will give an estimated cost for how long the query 
will take and how many rows will need to be scanned. Our login query is rather simple, 
so this may not yield anything, but it will be good to rule out an inefficient query plan.

**What is the state of our clusters?**

Have any nodes been down for any significant portion of time? Our system is configured 
to self-heal, so if nodes are down, what would be preventing them from firing up?

**Traffic surges?**

Did our system experience any spikes in traffic? If so, does this surge in traffic 
correlate with a known event (PR push, etc), or is this a possible sign of an attack?

We can check traffic spikes by looking at our server dashboard [WHICH ONE].

We are interested in looking at the logs for recent activity for the users who experienced the lag (or
any demographics we feel may have experienced this, based on our analysis above). 
From there, we can hone in on time windows we can use to assess spikes. If we're using 
the MySQL Workbench, which logs key performance indicators relevant to this triage,
including **client timing**, **network latency**, **server execution timing**, **index usage**, 
and **number of rows scanned**.

If we find there is a natural pattern of increased log-in that leads to bottlenecks, 
how can our load balancers and MySQL cluster provisioning be redesigned to handle such traffic?

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
which will indicate which directories in our code base changed in the container. 
If we see that log-in might have changed in some wayt  we can dive in further to 
diff those files in particular. Maybe there's a straighforward bug? 

### How we can we resolve this issue?

Let's say we found a bug that was introduced in a recent revsion. We could manually 
roll back to a previous version, but we must ask ourselves if restoring 
the previous low latency log-in for these users is more important than the benefits 
provided by other feautures included in our last revision (which will be undone if we rollback).
If we choose to rollback, here's how we might proceed. 

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

This will pull the bug out of production, and will allow us to deploy a functional 
version of our system while we address the next section (improving testing!).

### How might we test for such issues going forward? 

What is perhaps most alarming about this problem is that we did not catch it sooner. 
We had to wait until our users complained, which is much too late. 

It is possible our triage inspection will yield the results we are looking for, and the bug
can be fixed in short order. However, it may also be the case that the problem is more 
complex, and will require further troubleshooting. In either case we are going to want
more rigourous test coverage that replicates the conditions that led to the slow 
log-in our users experienced. For load balancing, we may wish to work with a tool 
like [Iago](https://github.com/twitter/iago), which excels at accurately replicating 
production traffic. 

Once we feel we have solved the problem and it passes our tests, including load testing, 
then we can set up a canary testing rollout to our nodes. This will requires us to 
set a timeframe under which revisions will be monitored before further rollout takes place. 
We should select time windows that afford the system a chance to monitor the kinds of interaction we expect
from our users. Given the volume we are assuming in this system, we can expect to see
most common activity within a 24 hour timeframe, or perhaps within an hour or minute. 
These rollouts can be timed based on the frequency of the processing they most directly 
address, or if the revision is more broad-reaching, than a typical range of user behaviors
should transpire during the monitoring phase.
