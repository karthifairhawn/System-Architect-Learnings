---
tags: [Learning]
title: Udemy
created: '2023-02-14T13:11:28.409Z'
modified: '2023-04-11T07:25:55.762Z'
---

# System Architect Learnings


## Architecht Consists
- Performance
- Scalability
- Reliability
- Security
- Deployement
- Technology Stack


---

# 1. Performance

The main goal is increase the performance of the system. So the following things are considered.
1. Latency
2. Concurrency
3. Caching
    
If any queue build up is occured in system, there might be performance issue. So finding the reason behind queue build up will helps in resolving issues in performance.
    
__Reasons for queue build-up.__
1. Ineffiecient slow processing.
2. Serial resource access.
3. Limited resource capacity.

``
    A request can be handled serially (Single threaded)(Once process at a time) in the cpu or concurrently.
``
__Performance Principle__

1. Efficiency
    - Resource Utilization
        - Memory utilization
        - CPU utilization
    - Logical analysis ( Delegated to developers)
        - Algorithms
        - DB Queries
    - Effective data storage
        - Data structures
        - DB Schema
    - Caching    

2. Concurrency ( Handling multiple requests simultaneously)
    - Hardware
    - Software
        - Queueing
        - Coherence

3. Capacity
    - Increasing the size of hardware will increase performance.

__System Performance Objective__

1. Minimize Latency.
    - Latency is measured in time units
    - Latency = Wait time + Process time

2. Maximise throughput
    - Rate of requests
    - Deponds on latency and capacity

**Metrics to measure performance**

1. Latency
2. THroughput
3. Errors
4. Resource Saturation
5. Tail Latency

**Reducing Network Latency**

1. Persistent Connections
2. Static data caching
3. Session/Data Caching
4. Connection Pook
5. Data Format & Compression in transfer





