---
title: MySQL 
menu:
    ai_notes:
        menu: Software Engineering
draft: True
---
#MySQL

I first encountered MySQL through my work at Avisell, where we stored data on airlines,
airports, and flight paths which we referenced in our ML prediction pipeline. I saw
that you could make and store tables, add and update records, and optimize SQL queries
to improve performance. That was the extent of my knowledge at the time. 

I saw that Yelp used MySQL clusters as the persistence backbone of their service,
and this got me thinking far more about how MySQL could grow and scale alongside
a distributed system. Could it really keep pace with Cassandra?

## B-Tree

It's the self-balancing tree data structure behind MySQL's indexing, so that reason
alone should inspire us to check it out. Also, it has a  B in its name that Wikipedia
says has unknown origins. Ooooo...mysterious.

Let's check it out. 
