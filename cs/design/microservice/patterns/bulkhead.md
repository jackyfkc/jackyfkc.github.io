Bulkhead 舱壁模式
---

Bulkhead isolates critical resources, such as connection pool, memory, and CPU, for each workload or service. By using bulkheads, a single workload (or service) can’t consume all of the resources, starving others. This pattern increases the resiliency of the system by preventing cascading failures caused by one service.


bulkhead, 是一种把自己从故障中隔离的方式. 在航运领域, 舱壁是船的一部分, 合上舱口后可以保护船的其他部分.


在软件架构中, 有许多不同的舱壁可供考虑.

关注点分离也是实现舱壁的一种方式. 通过把功能分解成独立的微服务, 降低了因为一个功能模块宕机而影响其他功能的可能性.


### When to use this pattern

Use this pattern to:

* Isolate resources used to consume a set of backend services, especially if the application can provide some level of functionality even when one of the services is not responding.

* Isolate critical consumers from standard consumers.

* Protect the application from cascading failures.
