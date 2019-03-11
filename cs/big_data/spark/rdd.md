Resilient Distributed Datasets
---

RDD, a distributed memory abstraction that lets us perform in-memory computations on large cluster.

Keeping data in memory can improve performance efficiently. RDD provide a restricted form of **shared memory**, based on **coarse-grained** transformations (e.g., map, filter and join) rather than fine-grained transformation.


## RDD Abstractions

Formally, an RDD is a read-only, partitioned collection of records. RDD can only be created through **deterministic operations** on either (1) data in stable storage or (2) other RDDs

