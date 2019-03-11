[PubSub](http://redis.io/topics/pubsub)
---
`SUBSCRIBE`, `UNSUBSCRIBE` and `PUBLISH` implement the Publish/Subscribe messaging paradigm where (citing Wikipedia) senders (publishers) are not programmed to send their messages to specific receivers (subscribers).

Rather, published messages are characterized into channels, without knowledge of what (if any) subscribers there may be. Subscribers express interest in one or more channels, and only receive messages that are of interest, without knowledge of what (if any) publishers there are.
