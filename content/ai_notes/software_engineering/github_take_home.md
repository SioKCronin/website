---
title: System design challenge
menu:
    ai_notes:
        parent: Software Engineering
---

## Question 1

**What properties of the CAP theorem would you prioritize for a cloud storage service 
(e.g. Amazon S3, Google Cloud Storage)? What tradeoffs would you have to make?**

I approach the consistency vs. availability trade-off as an opportunity to clarify
how our system might best serve our business goals. For example, in systems where 
it is mission-critical that all users see exactly the same data, such as 
systems serving critical-care patient medical records, then I would prioritize consistency. 
However, in services where users expect real-time access to information, such as Yelp "closing soon" 
restaurant recommendations, I would prioritize availability.

This has been my general approach in using the CAP theorem to address tradeoffs in database design, 
but I've been thinking recently about whether the Venn diagram used to depict this "theorem" 
is really accurate. RDBM systems are touted as achieving both consistency and availability while sacrificing
partition tolerance, but is that really true? Is partition tolerance ever a choice?
What was Dr. Eric Brewer really trying to say when he presented CAP theorem in 2000? I turned to Martin Klepperman 
[Please Stop Calling Databases CP or AP](https://martin.kleppmann.com/2015/05/11/please-stop-calling-databases-cp-or-ap.html) 
and Coda Hale's 
[You Can't Sacrifice Partition Tolerance](https://codahale.com/you-cant-sacrifice-partition-tolerance/) 
for answers, and here's what I learned. 

As Klepperman puts it, *partition tolerance* essentially means we are "communicating
over an asynchronous network that may delay or drop messages", and reminds us that 
"the internet and all datacenters have this property", so we don't really have a choice.
Hale puts this more directly when he states that "for a distributed system to not require
partition tolerance it would have to run on a network which is guarenteed to never 
drop messages (or deliver them late) and whose nodes are guarenteed to never die".
We don't live in such a world, so if we are to consider the context the database system
is operating in (which I believe we should), then some degree of partition tolerance
will be a part of any distributed system we design.

It's quite sobering to read through the precise definitions underlying the assertions
of the CAP theorem, and measure just how far those definitions are from the colloquial 
use of the same words. Take "availability" for instance. In the context of CAP, 
an available system is defined as one where "every request received by a non-failing node in the system must result
in a non-error response". This is a very limited view on avaiability, and says nothing of 
nodes that have crashed or are being recovered, software bugs, or systems that have
run out of space. There is a range of desired "availability" that extend beyond 
well beyond the scope of ensuring a resposne from a non-failing node. Turning to consistency, 
Hale reminds us that standard data replication is not "strongly
consistent" as there is inherent lag. Instaneous and global consistency in a distributed 
system is impossible, given the physical laws of the universe, but in practice we 
typically mean a reduction of lag to a level that is imperceptible. 

So, in regards to our cloud-hosted system, knowing that we are already working with
in a partition tolerant environment, I would want to ensure we are clear about the
specific conditions that would compromise the availability of our data (in the 
broader-than-CAP sense) while addressing the linearizability ("consistency") of
how updates propogate through our system and how these are experienced by our users.

## Question 2 
**You are part of a team that is responsible for a large, distributed web application. 
Assume the architecture consists of multiple services running on Kubernetes, using 
primarily MySQL for persistence, and some form of API and user-facing frontend. 
Make whatever other assumptions about the system you wish.**

We can assume we have frontend, processing, and database clusters running in each of our 
AWS service availability zones where we are servign customers. We can assume we have 
load balancers effectively handling traffic to our processing layer, and a CDN 
to cache all commonly requested content in these regions, with Least Recently Used (LRU) eviction strategy.
We may also have cache layer behind our servers to support common database lookups and processing requests. 

Our data modeling for our MySQL cluster can include a Users table, as well as tabels to 
store data and media pointers for all the other amazing things our system does. Writes 
to our database cluster can be processed by a master node cluster and written 
to our replicas. Reads can happen from any node. MySQL Workbench will be set up for DB monitoring,
and we will enable our **slow-log** by setting the appropriate parameters in the **my.cng** file. 
Our Users table will be indexed to ensure speedy lookup during log-in verification.

We will use Docker as our container service and Kubernetes as our container orchestrator.  

There are many aspects of our system we could explore, but in order to set up Question 3 well, 
let's address the following: 

#### Login

For login, our process can be that if a user is in the user index
and if the hash of their submitted password matches the stored value of their 
hashed password, then they are validated and a new session is created. For the hashing
we can use some form of cryptographic hashing function (i.e. Argon2), that is deterministic,
quick to compute, and infeasible to generate the original password from the hash.
This hashed password will be stored in our Users table, and compared
against the hash of the password used at login.

So, the login API might be something like
```
LOGIN(timestamp, IP, user, password)
```

which will send to our verification processor a JSON file.
```
{ timestamp: '1000-01-01 00:00:00', 
  IP: '127.0.0.1/32',
  user: SioKCronin,
  password: IHeartData
}
```

Our verification processor will then process the request.

```
import argon2
import mysql.connector

user, password = PARSE FROM JSON MESSAGE

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

For traffic volume, I'm going to use Yelp's traffic as an example, as their persistence
layer consists of primarily MySQL clusters backed up to Redshift, and they
also orchestrate their deployment of Docker containers with Kubernetes (combined with Mesos
in their in-house system, PaaSTA). 

Yelp sees an average of 100 million unique mobile users a month. If we estimate 
that 20% of Yelp's users stay logged into the app, these means
there are approximately 80 million users who log in each month.
If we assume the distribution of logins is constant across the entire day, that 
would mean an average of 925 logins/second. While Yelp is used globally, the lioshare
of its users are in the United States, and they most likely have observed hours of peak 
usage, so it would be safe to assume the number of logins per second could excede 
this initial estimate, perhaps extending up to tens of thousands of logins per econd. 

This means a large number of users could be negatively impacted by slow login, 
especially during peak hours, and, relatedly, any
rollout of software updates must take into account this steady, high-volume traffic. 

#### Container orchestration

Since we are using Kubernetes, our system is self-healing. If we have nodes down that are not auto-recovering,
this will point us either to our Kubernetes configuration itself or a problem with our hosted service.

#### Cloud Hosting and Monitoring

Let's assume we are using AWS, with a monitoring service like Prometheus for our cluster maintenance. 
We will set up a VPN with security groups based on the product ownership areas and 
the necessary restrictions for our team. 

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

**Which users have been affected?** 

It is imortant to note that users are reporting they are successfully
logging in, it is just taking much longer. 

How many users have reported this issue, and what do they have in common? Geography? 
Similar user names? Similiar log-in times? Android, IOS, desktop)? If similarities 
are encountered, what parts of our system do they point to? Do the similarities relate
to how our DB is sharded, thereby possibly indicating a problem in our load balancing or 
pointing to downtime on particular nodes in our cluster? Does the regionality of the issue point to possible
issues in our cloud hosting for that region?

To start investigating, we'll want to look at the slow-log we enabled for our MySQL cluster. 

```python
mysqldumpslow
```

This will give us a view of all recent slow queries, which, depending on the scope of the problem,
will most likely needed to be filtered further. We can do so by adding a few more flags,
such as **-i** for specific node instances (if we have identified any) or return only a select number **-t**.

We can also tag on an **EXPLAIN** to our query, and run it in our dev environment to 
check out our query plan. This will give an estimated cost for how long the query 
will take and how many rows will need to be scanned. Our login query is rather simple, 
so this may not yield anything, but it will be good to rule out an inefficient query plan.

**What is the state of our clusters?**

For this we can turn to Prometheus and our AWS dashboard. Have any nodes been down 
for any significant portion of time? Our system is configured to self-heal, so 
if nodes are down, what would be preventing them from firing up?

**Traffic surges?**

Did our system experience any spikes in traffic? If so, does this surge in traffic 
correlate with a known event (marketing push, etc), or is this a possible sign of an attack?

We can check traffic spikes by looking at our AWS dashboard, or whatever monitoring GUI
we have selected for our frontend metrics.

To help narrow in on time windows worth consider, we would be interested in 
looking at the logs for recent activity for the users who experienced the lag (or
any demographics we feel may have experienced this, based on our analysis above). 
In our MySQL Workbench, we would be interested in looking in teh logs 
at key performance indicators relevant to this triage, such as **client timing**, 
**network latency**, **server execution timing**, **index usage**, and **number of rows scanned**.

If we find there is indeed a pattern of non-malicious, naturally-occurring increase 
in logins that leads to bottlenecks, how can our load balancers and MySQL cluster 
partitioning be redesigned to handle such traffic?

**Was something recently deployed that correlates with this phenomena?**

If we have not encountered an obvious error in our clusters or anomalies in 
system traffic that would explain these log-in lags, it is time to evaluate when
did this change begin in order to debug it. Have we recently our code for handling logins? 

We can start but running a diff on the container itself

```
Docker diff CONTAINER_ID
```
which will indicate which directories in our code base changed in the container. 
If we see that login might have changed in some way, we can dive in further to 
look at the diff of those files in particular. Maybe there's a straighforward bug? 

### How we can we resolve this issue?

Let's say we found a bug that was introduced in a recent revsion. We could manually 
roll back to a previous version, but we must ask ourselves if restoring 
the previous low latency login is more important than the benefits 
provided by other feautures included in our last revision (which will be undone if we rollback).
If we choose to rollback, here's how we might proceed. 

Like 'git reset --hard commitID' in git version control, we can roll back
to a specific previous revision in the deployment history.

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
log-in our users experienced. For load testing, we may wish to move forward with a tool 
like [Iago](https://github.com/twitter/iago), which excels at accurately replicating 
production traffic. 

Once we feel we have solved the problem and it passes our tests, including load testing, 
then we can set Kubernets to use a canary testing rollout strategy. This will requires us to 
set a timeframe under which revisions will be monitored before further rollout takes place. 
We should select time windows that afford the system a chance to monitor the kinds of interaction we expect
from our users. Given the volume we are assuming in this system, perhaps we can expect to see
most common activity within a 24 hour timeframe, or perhaps within an hour or minute. 
Whatever we chose, these rollouts should be timed such that the new code is exposed
to a typical range of user behavior, so that we can effectively monitor performance.
