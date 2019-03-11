[Transaction](http://redis.io/topics/transactions)
----
Unlike transaction in relational database, Redis transaction is a weak version of regular transaction which satisfies ACID.

`MULTI`, `EXEC`, `DISCARD` and `WATCH` are the foundation of transactions in Redis.

A Redis transaction is entered using the `MULTI` command. The command always replies with OK. At this point the user can issue multiple commands. Instead of executing these commands, Redis will queue them.

> The implementation uses a `per-DB hash table` mapping keys to list of clients watching those keys. So that given a key that is going to be modified we can mark all the associated clients as dirty.

> Also every client contains a list of `WATCHed` keys so that possible to un-watch such keys when the client is freed or when `unWATCH` is called

``` C
typedef struct watchedKey {
    robj *key;
    redisDb *db;
} watchedKey;
```

_Refers to_

* [v4.0 source code](https://github.com/antirez/redis/blob/4.0/src/multi.c)
