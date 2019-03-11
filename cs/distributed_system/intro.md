分布式系统
-----

<div class="alert alert-info">
<p>
A distributed system is one in which the failure of a computer you didn't even know existed can render your own computer unusable.
</p>
<hr/>
<p>在一个系统中有一台你从未见过的机器出了问题, 却能致使你的机器也无法使用, 那么它就是一个分布式系统 ------ 莱斯利.兰伯特, 1987
</p>

</div>

- - -

为什么我们需要分布式系统？

* tolerate node failure 容忍节点故障

* scalability (processing more requests than a single machine) 扩展性

* latency (placing replicas geographically closer to users) 延迟

- - -

分布式系统的麻烦

* Unreliable Networks 不可靠的网络

    网络可能会丢包，乱序，超时

* Unreliable Clocks 不可靠的时钟

    不同机器的时钟不一致，另外时钟会出现偏移

- - -

Models describe the key properties of a distributed system in a precise manner.

* System model (synchronous, partially synchronous, asynchronous)

* Failure model (crash-fail, crash-recovery, Byzantine)

* Consistency model (strong, weak, eventual)

- - -

Theorem 定理 (maybe?)

* [FLP](flp.md)

    FLP proved that consensus cannot be achieved in asynchronous distributed systems if failures are possible.


* [CAP](cap.md)

    Available or Consistent when Partitioned

- - -

分布式系统一个首要问题是进程间通信

* RPC (Thrift, grpc, Rest/Http, Dubbo...)

* MQ (AMQP based: RabbitMQ; log based: Kafka)

- - -

其次，进程间需要同步：互斥（分布式锁）和分布式事务（原子提交）

* Distributed Lock

* [Distributed Transaction](transaction.md)


- - -

**共识算法 Consensus Algorithm**

Getting a group of nodes to agree on a given value is described as the `consensus problem`

共识问题: 一组节点就选择一个 value 达成共识 (single decree).


* [Paxos](paxos/intro.md)

* [Raft](raft/intro.md)

* [Zookeeper](zookeeper/intro.md)

* Etcd

- - -

分而治之

* Replication 副本

* Partitioning 分区


## 进一步阅读

Online Blog & Articles

* [Distributed Systems for fun and profit, mixu](http://book.mixu.net/distsys/single-page.html)

    概述分布式系统的多个主题


* Fallacies of Distributed Computing Explained

    L Peter Deutsch 在 Sun 公司发表的分布式计算的 7 个谬论

- - -

Books

* Martin Kleppmann: Designing Data Intensive Applications - The Big Ideas Behind Reliable, Scalable And Maintainable System

    设计数据密集型应用, 对于实践有非常好的指导价值, 建议作为入门读物


* Joe Armstrong: Making Reliable Distributed Systems in the presence of software errors

    中译本: 面对软件错误构建可靠的分布式系统


* Architect for Scale - High Availability For Your Growing Applications

- - -

* Andrew S. Tanebaum: Distributed Systems Principles And Paradigms

    中译本, 分布式系统原理与范型; 偏理论

* Distributed Operating Systems 分布式操作系统

* Introduction to Reliable and Secure Distributed Programming

* Nancy A. Lynch: Distributed Algorithms

- - -

How To Architect

* Kate Matsudaira: [Scalable Web Architecture and Distributed Systems](http://www.aosabook.org/en/distsys.html)

     This article seeks to cover some of the key issues to consider when designing large websites, as well as some of the building blocks used to achieve these goals.

* Google: Designs, Lessons and Advice from Building Large Distributed Systems

* Dan Pritchett: Architecting for Latency, eBay, October 2007


* Architecting for scale, Beautiful Architecture, Chapter 3

- - -

* [High Availability Concepts and Best Practices in Oracle](https://docs.oracle.com/cd/A91202_01/901_doc/rac.901/a89867/pshavdtl.htm)
