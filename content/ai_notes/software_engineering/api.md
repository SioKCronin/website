---
title: API
menu:
    ai_notes:
        parent: Software Engineering
---
Application Program Interfaces (APIs) do a lot of heavy lifting in software 
engineering, and are a world unto themselves. Let's cover the basics for 
interacting with an API, and then build out from there. 

## Designing an endpoint

An endpoint is one end of a communication channel. In the case of an API call,
the client may request data from a specific endpoint on a server. If we were 
designing that endpoint, we'd want to specify what information is required
in that API call to serve the data. Are their specific query terms? Do we need
the user's ID? Is the timestamp important? These inputs become parameters we'll
pass to our underlying logic to obtain the relelvant data. 

## GET vs. POST

GET is a common HTTP method, and used to request data from a specific resource. 

On the flipside, POST is used to send data to a server to create/update a resource.

## REST vs RPC

I'll admit, I fell victim to what Phil Stugeon describes in his article on RPC
(remote procedure call), which is I assumed REST would better suit my needs,
so I gave it little attention. Phil writes about [the difference between RPC
and REST](https://www.smashingmagazine.com/2016/09/understanding-rest-and-rpc-for-http-apis/), 
not in an attempt to prove one is more universally valuable than the other,
but to demonstrate situations where one might be more appropriate than the other.
RPCs excell at actions or commands, and Phil points out an example of RESTful API
that is being used to execute a command, and how this is really RPC in disguise. 
Can you think of a situation where you'd want RPC? My mind goes to situations
where you wouldn't need CRUD, but simply to execute a command - perhaps some
sensor-driven activation, like a trip-wire out in the world. 

And then Phil blows our minds and reminds us that we could, of course, have 
both RPC and REST for the same application! He also shows a clear example of
an RPC being used alongside a REST API, which is have an RPC to restart
servers and run commands on batches of servers (while the REST chugs on doing
its CRUD work). 






