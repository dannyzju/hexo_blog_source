---
title: 'System Design Topics: CAP Theorem'
date: 2020-03-21 10:19:52
tags:
- System Design
- CAP Theorem
---


CAP Theorem is a concept about distributed database system that we cannot build a general data store that is continually available, sequentially consistent, and tolerant to any partition failures. 
<!-- more -->
We can only build a system that has two of the following three guarantees:

- **Consistency**: Every read receives the most recent write or an error
- **Availability**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write
- **Partition tolerance**: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes

![CAP](https://www.researchgate.net/profile/Hamzeh_Khazaei/publication/282679529/figure/fig2/AS:614316814372880@1523475950595/Visualization-of-CAP-theorem.png)

However, in a distributed system, partitions can’t be avoided. So usually you'll need to make a software tradeoff between consistency and availability.

**CP - consistency and partition tolerance**

Waiting for a response from the partitioned node might result in a timeout error. CP is a good choice if your business needs require atomic reads and writes.

**AP - availability and partition tolerance**

Responses return the most recent version of the data available on a node, which might not be the latest. Writes might take some time to propagate when the partition is resolved.

AP is a good choice if the business needs allow for eventual consistency or when the system needs to continue working despite external errors.

*CAP Theorem was published in 1999, there're also some different options later on, see more readings:*

- [*A Critique of the CAP Theorem*](https://jvns.ca/blog/2016/11/19/a-critique-of-the-cap-theorem)
- [*CAP Twelve Years Later: How the "Rules" Have Changed*](https://www.infoq.com/articles/cap-twelve-years-later-how-the-rules-have-changed/)
