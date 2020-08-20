---
title: AWS Virtual Private Clouds (VPCs)
menu:
    ai_notes:
        parent: Serving Data
draft: False
---
### Overview

As J Cole Morrison puts it, we need Virtual Private Clouds (VPCs) because we need control
of security, the organization of our resources, traffic between our services, and the ability
to keep differing architectures separate. 

Some terms we'll need:

* **Subnets**:
* **Route Tables**:
* **Network ACLs**:
* **Internet Gateway**:
* **NAT Gateway**:
* **Variable-length subnet masking (VLSM)**: Allows you to specify arbitrary-lenght prefixes.
* **Classless Inter-Domain Routing (CIDR) block notation**: IP addresses consiste 
of two groups of bits; the most significant bits are the network prefix (identifies a 
whole network or subnet) and the least significant set forms the *host identifier* 
(specifies a particular interface of a host on that network). This notation includes
a suffix indidcating the number of bits of the prefix.

We first define a range of IP addresses for our VPC to sketch out the space we'll be building.

### Services
It's a big world of AWS services, so let's apply some cartography.

#### EC2

* **compute optimized**
* **memory optimized**
* **storage optimized**

#### S3 (Simple Storage Services)

* **Standard Storage**: Frequently accessed. Charged by the gibabyte used and
number of requests to access, delete, list, copy or loading data in S3. Less
than 1hr of downtime/yr.
* **Infrequent Access Storage**: Less than 9hrs of downtime/year.
* **Glacier**: Deep storage. Can take hours to retrieve. Much cheaper than standard.
Redundant data sites. 
* **Reduced Redundancy Storage**:

#### Elastic Load Balancer (ELB)

* Send client requests to appropriate server.
* Avoid server hotspots.
* **Classic Load Balancing**: Ensures fault tolerance int he event of an EC2 instance failure.
* **Application Load Balancing**: Looks at content request and routes accordingly. 

#### CloudFront

* Global content delivery system

#### Elastic Block Store (EBS)

* Low-latency instance access
* Access high speed Solid State Drive (SSD) storage.
* Layer security with Access Control Lists and encryption. 

### Amazon Route 53

* Domain Name System (DNS) routing.

### Cloudwatch

* Gather logs and monitor metrics.

### Elasticache

* Like Memcached or Redis

### Other

* **Lambda**: Abstracts AWS infrastructure. 
* **AWS Config**: Infrastructure management.
* **Elastic Beanstalk**: App development.
* **CloudTrail**: API transaction analytics.
* **Elastic File System (EFS)**: Grow and shrink file storage system. Can mount one file system
to multiple EC2 instances to share common data.
* **Kinesis**: Loading and analyzing streaming data. *Kinesis Firehose* ingests data. 
*Kinesis Analytics* collects data with SQL queries. *Kinesis Streams* transform data into 
dashboard or generate alerts. 



