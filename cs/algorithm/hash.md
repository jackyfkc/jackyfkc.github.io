哈希 Hashing
---
A hash function is any function that can be used to map data of arbitrary size to data of fixed size.


## Consistent Hashing 一致性哈希

Karger at " Consistent hashing and random trees: Distributed caching protocols for relieving hotspots on the World Wide Web" introduced the concept of consistent hashing and gave an algorithm to implement it. Consistent hashing specifies a distribution of data among servers in such a way that servers can be added or removed without having to totally reorganize the data. It was originally proposed for web caching on the Internet, in order to address the problem that clients may not be aware of the entire set of cache servers.

Karger 在论文 " Consistent hashing and random trees: Distributed caching protocols for relieving hotspots on the World Wide Web" 中首次提出一致性哈希概念并给出了实现的算法. 一致性哈希实现了数据在一组服务器上分布的方式, 使得 server 的添加和移除不需要数据全部重置. 早期是为了解决互联网上的 web 缓存问题, 使得 client 不需要感知到整个缓存服务器集合


Consistent hashing is a special kind of hashing such that when a hash table is resized, only `K/n` keys need to be remapped on average, where `K` is the number of keys, and `n` is the number of slots.

In contrast, in most traditional hash tables, a change in the number of array slots causes nearly all keys to be remapped because the mapping between the keys and the slots is defined by a modular operation.

The consistent hashing concept also applies to the design of distributed hash tables (DHTs). DHTs use consistent hashing to partition a key-space among a distributed set of nodes, and additionally provide an overlay network that connects nodes such that the node responsible for any key can be efficiently located.



## [Rendezvous Hashing](https://en.wikipedia.org/wiki/Rendezvous_hashing)

Rendezvous hashing, designed at the same time as consistent hashing, achieves the same goals using the very different Highest Random Weight (HRW) algorithm.


Rendezvous or highest random weight (HRW) hashing is an algorithm that allows clients to achieve distributed agreement on a set of `k` options out of a possible set of `n` options.

A typical application is when clients need to agree on which sites (or proxies) objects are assigned to. When `k` is 1, it subsumes the goals of consistent hashing, using an entirely different method.



## References

* Consistent hashing and random trees: Distributed caching protocols for relieving hot spots on the World Wide Web. In Proceedings of the 29th ACM Symposium on Theory of Computing (STOC), pages 654­663, 1997.

* John Lamping, Eric Veach: A Fast, Minimal Memory, Consistent Hash Algorithm

* Chord: A scalable peer-to-peer lookup service for internet applications
