Paxos
---
Assume a collection of processes that can propose values. A consensus algorithm ensures that a single one among the proposed values is chosen.

假定一组进程可以提交 value, 一致性算法需要确保在提交的 value 中有且只有一个 value 被选定.

Paxos 最先由 Leslie Lamport 在 1990 提交的一篇别出心裁的论文中描述, 最终在 1998 年正式发表, 标题为 "The Part-Time Parliament".


Assume that agents can communicate with one another by sending mes- sages. We use the customary asynchronous, non-Byzantine model, in which:

* Agents operate at arbitrary speed, may fail by stopping, and may restart. Since all agents may fail after a value is chosen and then restart, a solution is impossible unless some information can be remembered by an agent that has failed and restarted

* Messages can take arbitrarily long to be delivered, can be duplicated, and can be lost, but they are not corrupted


There are three roles in the consensus algorithm be performed by three classes of agents: _proposers_, _acceptors_, and _learners_: proposers that can propose values, acceptors that choose a single value, and learners that learn what value has been chosen.

在 Paxos 算法中有 3 种角色, _Proposer_, _Acceptor_, and _Learner_: _proposers_ 可以提议一个 value, _acceptors_ 从中选择一个 value, _learner_ 学习哪个 value 被选择.


- - -

* [Simple Paxos](simple_paxos.md)

* [Fast Paxos](fast_paxos.md)

* [Multi Paxos](multi_paxos.md)



Further Readings
---

* [Paxos Lecture](https://www.youtube.com/watch?v=JEpsBg0AO6o)

    Raft 作者 Diego Ongaro 写的 Paxos PPT, 极大降低了理解 Paxos 的门槛

- - -

* [Paxos Made Simple](http://lamport.azurewebsites.net/pubs/pubs.html#paxos-simple)

* [Fast Paxos](http://lamport.azurewebsites.net/pubs/pubs.html#fast-paxos)

* Vertical Paxos and Primary-Backup

* [Leslie Lamport's Writings](http://lamport.azurewebsites.net/pubs/pubs.html#lamport-paxos)

- - -

* [Using Paxos to Build a Scalable, Consistent, and High Available Datastore](https://arxiv.org/pdf/1103.2408.pdf)

* Paxos Made Live - An Engineering Perspective

    Google 参考 Paxos 实现 Chubby 的经验之谈

- - -

* [Clustering By Consensus](http://aosabook.org/en/500L/clustering-by-consensus.html)

    Python 实现的 500 行左右的 Demo
