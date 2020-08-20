---
title: Load Balancing Algorithms
menu:
    ai_notes:
        parent: Networking
---
First of all, the load balancer has to keep track of which servers are healthy
by routinely pinging them and recording if they respond. If a server fails
a health check, it is removed from the viable server list, and will only be 
added again if it passes a later health check.

## Algorithms

### Least Connection Method
LB directs traffic to the server with the fewest active connections

### Least Response Time Method
LB directs traffic to the server with the fewest active connections and the lowest
average response time. 

### Least Bandwidth Method
LB directs traffic to the server currently serving the least amount of traffic, 
measured in Mbps (megabits per second). 

### Round Robin Method
LB cycles through a list of servers and sends each new request to the next server.

### Weighted Round Robin Method
Weight servers based on their processing capacities. Higher weighted servers
are attempted first. 

### IP Hash
LB calculates hash of the client IP address, and uses that hash to determine
which server will receive the traffic.

## Software
In addition to open source load balancers like **HAProxy**, there are costly 
hardware load balancers like **NetScaler** that are highly effective. 
