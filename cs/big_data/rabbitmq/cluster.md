[Cluster](https://www.rabbitmq.com/clustering.html)
---

## Failure Handling
...


## Nodes

A node can be a `disk node` or a `RAM node`. RAM nodes are a special case that can be used to improve the performance clusters with high queue, exchange, or binding churn.

`RAM nodes` keep their `metadata` only in memory.

> Note that since persistent queue data is always stored on disc, the performance improvements will `affect only resource management` (e.g. adding/removing queues, exchanges, or vhosts), but `not publishing or consuming speed`.

