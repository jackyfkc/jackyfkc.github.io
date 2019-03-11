Cassandra
---

Official pronunciation: \kə-ˈsan-drə\

Apache Cassandra is a highly-scalable partitioned row store. Rows are organized into tables with a required primary key.

Apache Cassandra 是 Facebook 构建的一个可扩展的基于分区的行式存储系统.


Cassandra originated at Facebook in 2007 to solve that company’s inbox search problem, in which they had to deal with large volumes of data in a way that was difficult to scale with traditional methods. Specifically, the team had requirements to handle huge volumes of data in the form of message copies, reverse indices of messages, and many random reads and many simultaneous random writes.

Cassandra 由 Facebook 在 2007 年设计实现用来解决海量数据搜索问题. 它是一个 P2P 的数据存储系统, 数据模型类似于 Google BigTable, 架构类似于 Amazon Dynamo, 系统只提供最终一致性.


- - -

* [Data Modeling](data_model.md)

* [Query Language](cql.md)

- - -

* [Architecture](architecture.md)

* [Read and Write Path](read_and_write_path.md)



## Further Readings

Online Articles & Lectures

* Dynamo: Amazon’s Highly Available Key-value Store

* Avinash Lakshman, Prashant Malik: Cassandra - A Decentralized Structured Storage System

* Ion Stoica, Robert Morris...: Chord: A scalable peer-to-peer lookup protocol for internet applications. 2003.

* Matt Welsh, David Culler, and Eric Brewer. SEDA: An architecture for well-conditioned, scalable internet services. 2001

* Xavier D ́efago...: The ϕ Accrual Failure Detector. 2004

* Robbert van Renesse,...: Efficient reconciliation and flow control for anti-entropy protocols. 2008.

- - -

Books

* Cassandra: The Definitive Guide

* [Cassandra: The Definitive Guide, 2nd Edition Book Review and Interview](https://www.infoq.com/articles/cassandra-2nd-edition-book-review)

- - -

* [Source Code on GitHub](https://github.com/apache/cassandra)
