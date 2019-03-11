[Distributed Lock](http://redis.io/topics/distlock)
---

* `Safety property`: Mutual exclusion. At any given moment, only one client can hold a lock.

* `Liveness property A`: Deadlock free. Eventually it is always possible to acquire a lock, even if the client that locked a resource crashed or gets partitioned.



Version 1: Locking with [SETNX](https://redis.io/commands/setnx)
---

`SETNX` can be used as a locking primitive. For example, to acquire the lock of key `foo`, the client could try the following

    SETNX lock.foo <current Unix timestamp + lock timeout + 1>


In order to making this locking mechanism more robust, a client holding the lock should always check the timeout did not expire before unlocking the key with DEL because client failures can be complex, not just crashing but also blocking a lot of time against some operations and trying to issue DEL after a lot of time (when the LOCK is already held by another client)


## Handling deadlocks

What happens if a client fails, crashes, or is otherwise not able to release the lock?



Version 2:
---

Another property added here

* `Liveness property B`: Fault tolerance. As long as the majority of Redis nodes are up, clients are able to acquire and release locks.




_Refers to_

* [Is Redislock safe?](http://antirez.com/news/101)

* [Distributed locks with Redis](https://redis.io/topics/distlock)
