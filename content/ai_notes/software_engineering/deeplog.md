---
title: DeepLog
menu:
    ai_notes:
        parent: Software Engineering
draft: True
---
DeepLog: Anomaly Detection and Diagnosis from System Logs through Deep Learning
([pdf](https://acmccs.github.io/papers/p1285-duA.pdf))

Holy smokes, this is a fun paper! 

The methods used here build from the premise that "entries in a system log are 
a sequence of events produced by the execution of structured source code (and 
hence can be viewed as a structured language". That's worth pausing to consider.

When are system logs generated? Well, if we reference **syslog**, an industry 
standard originally developed by Eric Allman in the '80s, we see that each entry
includes a facility code and a severity level, as well as a header that includes
things like originator process ID, timestamp, and hostname/IP. So, since the log
records what we've asked it to, we can read it as a story of what happened, or, 
better yet, we can train our model to learn its words and syntax and tell us when
things look normal and when we're deviating from the script. 

The two key contributions with this paper are the leverating of an LSTM network
to train DeepLog with minimal data and get it up and running as an online anomaly 
detector, as well as DeepLog's ability to diagnose problems based on the workflow
models it develops in training. Super cool.

So, how does it work? 

## Setup

### Log parser

### DeepLog architecture

### Threat model

## Anomaly detection 

### Execution path anomaly 

### Parameter value and performance anomaly 

### Online weight updating

## Workflow construction

The first need here is to separate log entries for different tasks. 
