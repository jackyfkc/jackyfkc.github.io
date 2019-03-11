writing...

Here I want to provide a general purpose version of TCP based connection pool.

> Why connection pool is critical useful? It is because the creation of TCP connection is expensive(Three-way handshake + Slow Start).


Design Goal
---

* Thread Safe

* Fork Safe


**Note:** A reused connection is stateful.



Handling Failover
---
...



Health Monitoring
---
...


Refers to...
