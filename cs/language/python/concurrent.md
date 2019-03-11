In CPython, we can use process, thread, coroutine to implement concurrency programming.

在 CPython 中, 我们可以使用进程, 线程以及协程来实现并发.


## Process
...




## Thread

Python's global interpreter lock prohibits running Python code in parallel in one process anyway. Parallelizing CPU-bound algorithms in Python requires multiple processes, or writing the parallel portions of the code in C.



### Signal

It is crucial to understand that there is a low-level (C) signal handler and a high-level (Python) signal handler.

A Python signal handler does not executed inside the C signal handler. Instead, when a signal received, the C signal handler set a flag which tell the VM to execute the corresponding Python signal handler at a later point (for example, at the next bytecode instruction).


The reason why I put this section here is because Python signal handler are always executed in the main Python thread, even if the signal was received in another thread.

Besides, only the main thread is allowed to set a new signal handler.

Python 的信号处理函数只能在主线程中执行, 即使信号是在其他线程中接收的. 此外, 只有主线程可以设置信号处理函数.


## Coroutine

The are two ways to implement coroutine in CPython, `gevent` and `yield` (e.g. Tornado)



## Hybrid

The best solution to implement concurrent programming is the combination of process and coroutine.



## Reference

* Programming with Posix Threads

* [Jython Concurrency](http://www.jython.org/jythonbook/en/1.0/Concurrency.html)
