[LRU cache](http://redis.io/topics/lru-cache)
---

Initially Redis had no support for LRU eviction. It was added later, when memory efficiency was a big concern.

Redis LRU algorithm is not an exact implementation for some reasons.

> Redis use 24 bits in the object to store the least significant bits of the current unix time in seconds.

How to select
the key with the greatest idle time in order to evict it?

> And the initial Redis algorithm was quite simple: when there is to evict a key, select N random keys, and evict the one with the highest idle time.


In order to improve something, antirez write tools that simulate different workloads, and check the hit/miss ratio

>

Least Frequently Used


_Refers to_

* [Random notes on improving the Redis LRU algorithm](http://antirez.com/news/109)

