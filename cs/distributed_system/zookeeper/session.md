Session
---
A client connects to ZooKeeper and initiates a session. Once a connection to a server is established, a `session ID` is assigned to the client. Sessions have an associated timeout. The client will send heartbeats to the server to keep the session valid.

ZooKeeper considers a client faulty if it does not receive anything from its session for more than that timeout. A session ends when clients explicitly close a session handle or ZooKeeper detects that a clients is faulty, and the `session ID` will become invalid.

Within a session, a client observes a succession of state changes that reflect the execution of its operations. **Sessions enable a client to move transparently from one server to another within a ZooKeeper ensemble, and hence persist across ZooKeeper servers**.



## Session tracking

Rather than tracking sessions exactly, Zookeeper track them in batches. That are processed at fixed intervals. This is easier to implement than exact session tracking and it is more efficient in terms of performance. It also provides a small grace period for session renewal.



## Further Readings

* [ZooKeeper-1147 Issue Jira: Add support for local sessions](https://issues.apache.org/jira/browse/ZOOKEEPER-1147)

    This improvement is in the bucket of making ZooKeeper work at a large scale. We are planning on having about a 1 million clients connect to a ZooKeeper ensemble through a set of 50-100 observers. Majority of these clients are read only - i.e., they do not do any updates or create ephemeral nodes.

