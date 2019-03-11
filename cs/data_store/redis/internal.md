[Internal](https://github.com/antirez/redis#redis-internals)
---

Redis is single threaded, actually, Redis is *kinda* single threaded, since there are threads in order to perform certain slow operations on disk.

Redis 是单线程的, 但事实上, Redis 只是 *近似* 单线程, Redis 利用了多线程来处理一些慢操作

In a single-threaded server the easy way to make operations non-blocking is to do things incrementally instead of stopping the world. LRU eviction and keys expires are two obvious examples.

在一个单线程服务上, 实现非阻塞最简单的方式就是增量式的执行操作, 而不是 stop the world (姑且翻译成: 让世界停止转动). LRU eviction 和 key expires 是二个典型的例子, dict hash resize 也是增量式实现的.


**Redis Object**

``` C
typedef struct redisObject {
    unsigned type:4;
    unsigned encoding:4;

    /* LRU time (relative to server.lruclock) or
     * LFU data (least significant 8 bits frequency
     * and most significant 16 bits decreas time). */
    unsigned lru:LRU_BITS;
    int refcount;
    void *ptr;
} robj;
```

* [Anatomy of a Redis command](https://github.com/antirez/redis#anatomy-of-a-redis-command)



[Protocol](http://redis.io/topics/protocol)
---
...
