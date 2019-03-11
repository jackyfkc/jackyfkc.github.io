But the fundamental shortcoming of lock-based programming is that locks and condition variables do not support modular programming. By “modular programming,” I mean the process of building large programs by gluing together smaller programs. Locks make this impossible.


基于锁的编程, 其最根本缺陷在于, 锁和条件变量不支持模块化编程. 这里的"模块化"编程 是指粘合多个小程序来构建大程序. 基于锁的编程无法做到这一点.



## Lock Liveness

二个常见的活跃性问题


### 死锁 Dead Lock
...



### 活锁 Live Lock

A situation in which some critical stage of a task is unable to finish because its clients perpetually create more work for it to do after they have been serviced but before it can clear its queue.

Differs from `deadlock` in that the process is **not blocked or waiting for anything**, but has a virtually infinite amount of work to do and can never catch up.



### Re-entrant Lock
...


### Condition Variable 条件变量

For some reason, a thread may have to block itself because of its request may not complete immediately. This waiting for an event (e.g., I/O completion) to occur is realized by condition variables.

**A condition variable indicates an event** and has no value. More precisely, one cannot store a value into nor retrieve a value from a condition variable.

If a thread must wait for an event to occur, that thread waits on the corresponding condition variable. If another thread causes an event to occur, that thread simply signals the corresponding condition variable. Thus, **a condition variable has a queue for those threads that are waiting the corresponding event to occur to wait on**.


There are only two operations that can be applied to a condition variable: `wait` and `signal`.


Any thread that intends to `wait` on `condition` has to

1. acquire a mutex, on the same mutex as used to protect the shared variable

2. execute `wait`. The wait operations **atomically** release the mutex and suspend the execution of the thread.

> A condition variable `wait` always returns with the mutex locked.


When the condition variable is notified, a timeout expires, or a spurious wakeup occurs, the thread is awakened, and the mutex is atomically reacquired. The thread should then check the condition and resume waiting if the wake up was spurious.

> Condition variables are for signaling, not for mutual exclusion.

Condition variables do not provide mutual exclusion. You need a mutex to synchronize access to the shared data.


Why isn't the mutex created as part of the condition variables?

1. mutexes are used separately from any condition variables

2. It is common for one mutex to have more than one associated condition variable



### Event
...


### Semaphore
...

The semaphore concept was invented by Dutch computer scientist `Edsger Dijkstra` in 1962 or 1963



## Thread Pools

...


## Best Practice

* Keep the concurrency simple.

* Use tasks, which can be mapped to a thread pool.

* Use immutable objects where possible.

* Avoid unnecessary sharing of mutable objects.

* Minimize sharing of mutable objects. Queues and related objects – like synchronization barriers – provide a structured mechanism to hand over objects between threads. This can enable a design where an object is visible to only one thread when its state changes.

* Code defensively. Make it possible to cancel or interrupt tasks. Use timeouts.


## References

