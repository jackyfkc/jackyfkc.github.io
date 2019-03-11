[ZooKeeper](https://zookeeper.apache.org/)
---

ZooKeeper: Because Coordinating Distributed Systems is a Zoo


ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services; inspired by Google Chubby.



[Overview](https://cwiki.apache.org/confluence/display/ZOOKEEPER/ProjectDescription)
---

ZooKeeper 的设计尽可能满足数据一致性和可用性, 在发生网络分区的时候也提供了只读能力


Name service and configuration are two of the primary applications of ZooKeeper. These two functions are provided directly by the ZooKeeper API.


![zookeeper service](images/zookeeper_service.png)
*来源 [ZooKeeper Documentation: Overview - Design Goals](https://zookeeper.apache.org/doc/r3.4.12/zookeeperOver.html#sc_designGoals)*


- - -

**Programmer's Guide**

* [Data Model](data_model.md)

* [Session](session.md)

* [Watch](watch.md)

* [FAQ](faq.md)

- - -

**Anatomy**

* [ZooKeeper Server](zookeeper_server.md)

* [Zab](zab.md)

* [Client Protocol](client_protocol.md)


Further Readings
---

Books

* Zookeeper: Distributed Process Coordination

- - -

Online Articles & Documents

* The Chubby lock service for loosely coupled distributed systems

* [ZooKeeper: Wait-free coordination for Internet-scale systems](https://www.usenix.org/legacy/event/atc10/tech/full_papers/Hunt.pdf)

* Kenneth P. Birman and Thomas A. Joseph, "Exploiting virtual synchrony in distributed systems"

* [Zookeeper Official Document](https://zookeeper.apache.org/doc/r3.4.11/)

* [ZooKeeper Programmer's Guide](https://zookeeper.apache.org/doc/r3.4.9/zookeeperProgrammers.html)

    A client application developer's guide to Zookeeper

* [ZooKeeper Recipes and Solutions](https://zookeeper.apache.org/doc/r3.4.9/recipes.html)

    A guide to creating higher-level constructs with ZooKeeper


* [ZooKeeper Administrator's Guide](http://zookeeper.apache.org/doc/r3.4.11/zookeeperAdmin.html)

    A guide to Deployment and Administrator


- - -

Tools & Source Code

* [ZooKeeper Source Code](https://github.com/apache/zookeeper)

* [zk-traffic](https://github.com/twitter/zktraffic)
