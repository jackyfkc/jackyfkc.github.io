Architecture
----

![Kafka Cluster](images/kafka_cluster.png)
*来源: [Kafka 0.8.1 Official Document](https://kafka.apache.org/081/documentation.html)*


## Design principles

### Simple storage

Each partition of a topic corresponds to a logical log. Physically, a log is implemented as a set of segment file of approximately the same size.

<div class="alert">
For better performance, Kafka flush the segment files to disk ony after a configurable number of messages have been published or a certain amount of time has elapsed.
</div>

A message is addressed by a log offset.


### Efficient transfer

* Batch Send and fetch

* Rely on file system page cache, mostly, sequential access patterns

* Zero-copy transfer: file -> socket


### Stateless broker

In Kafka, the information about how much each consumer has consumed is not maintained by the broker, but by the consumer itself.


## Guarantees

At a high-level Kafka gives the following guarantees:

* Messages sent by a producer to a particular topic partition will be appended in the order they are sent. That is, if a record `M1` is sent by the same producer as a record `M2`, and `M1` is sent first, then `M1` will have a lower offset than `M2` and appear earlier in the log.

* A consumer instance sees records in the order they are stored in the log.

* For a topic with replication factor `N`, we will tolerate up to `N-1` server failures without losing any records committed to the log.
