Replication
---
MongoDB's replication facility, provides

* automatic fail-over

* data redundancy

A replica set is a group of `mongod` instances that maintain the same data set.


Replica sets rely on two basic mechanisms: an `oplog` and a `heartbeat`.

* The `oplog` enables the replication of data, and

* the `heartbeat` monitor health and triggers fail-over.


## The OPLOG

The `oplog` is a `capped collection` that lives in a database called `local` on every replicating node and records all changes to the data.

Each `oplog` entry is identified with a `BSON timestamp`, and all secondaries use the timestamp to keep track of the latest entry they've applied.



## [Replica Set Elections](https://docs.mongodb.com/manual/core/replica-set-elections/)

Replica sets use `elections` to determine which set member will become primary. Elections occur after initiating a replica set, and also any time the primary become unavailable.

The `primary` is the only member in the set that can accept `write` operations.

<div class="alert alert-warn"> While an election is in process, the replica set has no primary and cannot accept writes and all remaining members become read-only
</div>

