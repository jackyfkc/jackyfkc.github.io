[Protocol](https://kafka.apache.org/protocol)
---
The Kafka protocol is fairly simple, there are only 6 core client requests APIs.

Kafka uses a binary protocol over TCP. The protocol defines all apis as request response message pairs. All messages are size delimited and are made up of the following primitive types.


## APIs

基于 [KafkaApis.scala, v0.11.0.0](https://github.com/apache/kafka/blob/0.11.0.0/core/src/main/scala/kafka/server/KafkaApis.scala)


### Most Common APIs

* PRODUCE

* FETCH

* METADATA


### Offset Management

* OFFSET_COMMIT

* OFFSET_FETCH

* LIST_OFFSETS


### Consumer Group Management

* JOIN_GROUP

* LEAVE_GROUP

* SYNC_GROUP

* LIST_GROUPS

* DESCRIBE_GROUPS


### Admin Related

* CREATE_TOPICS

* DELETE_TOPICS



### Transactional Related

* ADD_PARTITIONS_TO_TXN

* ADD_OFFSETS_TO_TXN

* END_TXN

* WRITE_TXN_MARKERS

* TXN_OFFSET_COMMIT



## Further Readings

