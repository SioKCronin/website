---
title: "DeepLog: Anomaly Detection and Diagnosis from System Logs through
Deep Learning"
date: "2018-07-16"
---
**DeepLog: Anomaly Detection and Diagnosis from System Logs through Deep Learning**
by Min Du, Feifei Li, Guineng Zheng, & Vivek Srikumar (2017). 

## Overview

Inspired by natural language modeling, the authors present a deep learning approach
to anomaly detection in system logs.

## Key concepts

* **system logs**: A file that records the system states and significant 
events for debugging software. 
* **syslog**: The system log standard maintained by Internet Engineering Task Force (IETF). 
This enables a standard system that generates, filters, records, and analyzes log messages. 
Check out the [protocol](https://tools.ietf.org/html/rfc5424) for more info.
* **online monitoring**: Processing data in real-time from a data stream.
* **Long Short-Term Memory (LSTM)**: This recurrent neural network (RNN) building block
uses a gating system (input, output, and forget gates) which enable patterns to be detected
over arbitrary time intervals (not just from the contiguous context). 

## How it works

Training data are parsed to key-value (k-v) vectors which are used to construct the 
system exectution workflow model and train the anomaly detector. The key is the 
string constant from the print statement in the source code which printed the error
message (i.e. if the statement was "Ran in 5 seconds", then k = Ran in * seconds). 
The * value(s) are combined with the time since last error message into a k's associated
v vector, the latter being used to detect performance anomalies. 

For the detection phase, new entries are parsed as in training, and checks to see 
if the log key is normal. If it is, then the value vector is assessed by the 
anomaly detector, so the system is checking both key and value for anoalies. 
If an anomaly is indeed detected, the workflow model will provide a useful context 
for diagnosis. 

The input into DeepLog is the stream of log entries, and the output is the probability
distribution of the next source code statement to appear (this is how anomaly detection 
is generated).

## Key contributions

* Online method.
* There is a parameter value anomaly detection model defined for each key, which advances
on previous methods that only evaluated key anomalies.
* If False Positives are detected, the anomaly detection model can be updated with 
this new, correctly-labeled pattern.
