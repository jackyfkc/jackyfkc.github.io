Concept
---



## Lock Free

...


## Wait Free


wait-free is that each thread is guaranteed to correctly compute its operations in a bounded number of its own steps, regardless of the actions, timing, interleaving, or speed of the other threads. This bound may be a function of the number of threads in the system; for example, if ten threads each execute the `CasCounter.increment()` operation once, in the worst case each thread will have to retry at most nine times before the increment is complete

