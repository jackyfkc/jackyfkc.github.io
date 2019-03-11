Consumer
---
The Kafka consumer works by issuing `fetch` requests to the brokers **leading** the partitions it wants to consumer. The consumer specifies its offset in the log with each request and receives back a chunk of log beginning from that position.


## Push vs Pull

* A push-based system has difficulty dealing with diverse consumers as the producer controls the rate at which data is transferred.

    The goal is generally for the consumer to be able to consume at the maximum possible rate.

    A pull-based system has the nicer property that the consumer simply falls behind and catches up when it can


* Another advantage of a pull-based system is that it lends itself to aggressive batching of data sent to the consumer.


* The deficiency of a naive pull-based system is that if the producer has no data the consumer may end up polling in a tight loop, effectively busy-waiting for data to arrive.


## Consumer Group

![Kafka Consumer Group](images/kafka_consumer_group.png)



### Consumer re-balancing algorithm
...
