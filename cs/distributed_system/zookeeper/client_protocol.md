Messaging Protocol
---

When describing the ZooKeeper messaging protocol we will talk of packets, proposals, and messages:

当描述 ZooKeeper 消息协议时, 我们需要以下术语


## Concepts

**Packet 包**

a sequence of bytes sent through a FIFO channel

**Proposal 提议**

a unit of agreement. Proposals are agreed upon by exchanging packets with a quorum of ZooKeeper servers. Most proposals contain messages, however the `NEW_LEADER` proposal is an example of a proposal that does not correspond to a message.

**Message 消息**

a sequence of bytes to be atomically broadcast to all ZooKeeper servers. A message put into a proposal and agreed upon before it is delivered.


## Phase

ZooKeeper messaging consists of two phases: ZooKeeper 消息协议包括二个阶段

**Leader activation**

In this phase a leader establishes the correct state of the system and gets ready to start making proposals.

**Active messaging**

In this phase a leader accepts messages to propose and coordinates message delivery.


### Leader Activation
...


## Knowledge Base for Client

### Connection failures can make creating ephemeral-sequential nodes difficult

When creating an ephemeral-sequential, clients need to get the actual name of the node created (i.e. the requested `ZNode` name plus its sequence number). However, if there is an edge case whereby the server will successfully create the ephemeral-sequential node but the client will not get the result (due to partitioning, etc.). If the client reconnects before the session expires, the newly created ephemeral-sequential will still exist and wreak havoc with the recipe.

A good workaround for this issue is to include a GUID/UUID in the ZNode name. If there is a `KeeperException` during node creation, wait until successful re-connection, call `getChildren` and search for a `ZNode` the contains the GUID/UUID in its name. If found, you can be sure that this was the node you previously created.


### Connection failures can make deleting nodes difficult

Most of the ZooKeeper recipes involve creating a ephemeral-sequential node and then deleting that node to signal that another client can take over (etc.). If, while trying to delete the node, there is a network partition, etc. the node deletion will fail. If the client reconnects before the session expires, however, the ephemeral node will not expire.

A good workaround for this is to have a deletion queue/thread. Nodes that need deleting are added to the queue. If a `KeeperException` is thrown during delete, the node is added back to the queue for eventual deletion.


### Implement a retry mechanism

As the ZooKeeper docs make clear, there are a number of "recoverable" exceptions that clients must deal with. In particular, `ConnectionLossException` and `SessionExpiredException`.

Good ZooKeeper client applications are designed to account for failure. Your ZooKeeper ensemble will experience connection problems in production. Therefore, so your recipes should account for this. A retry mechanism that catches `ConnectionLossException`, etc. and retries operations as appropriate is highly advised.


## Reference

* [Knowledge Base for Client and Binding Implementations](https://cwiki.apache.org/confluence/display/ZOOKEEPER/Knowledge+Base+for+Client+and+Binding+Implementors)
