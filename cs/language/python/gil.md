[GIL](https://docs.python.org/2/glossary.html#term-global-interpreter-lock)
---

CPython has a `global interpreter lock` (locking the entire interpreter), is a `mutex` that prevents multiple native threads from executing Python byte codes at once.

CPython 有个全局解释器级别的锁, 简称 GIL, 用于防止多个线程同时执行 Python 字节码


## Thread State and GIL

This lock is necessary mainly because CPython's memory management is not thread-safe. (However, since the GIL exists, other features have grown to depend on the guarantees that it enforces.)

之所以需要这个锁, 主要是因为 CPython 的内存管理不是线程安全的 (另一方面, 因为 GIL 的存在, 其他功能块开始依赖于它)

Without the lock, even the simplest operations could cause problems in a multi-threaded program: for example, when two threads simultaneously increment the reference count of the same object, the reference count could end up being incremented only once instead of twice.

在多线程程序中, 没有 GIL, 即使是最简单的操作也可能会导致问题; 比如:当二个线程同时去累加同一个对象的引用计数时, 最终引用计数可能只被累加一次而不是二次

<div class="alert alert-info">
For performance reason, a single big lock is a bad idea :-(
</div>


In order to support multi-threaded Python programs, in Python 2.7 and early version, the interpreter regularly releases and reacquires the lock -- by default, every 100 bytecode instructions (this can be changed with `sys.setcheckinterval()`).

为了支持多线程, 在 Python 2.7 和早期版本, 解释器有规律的释放和获取 GIL - 默认情况下, 每执行 100 个指令 (这个值可以通过 `sys.setcheckinterval` 来修改)


### Releasing the GIL from extension code

Note: some extension modules, either standard or third-party, are designed so as to release the GIL when doing computationally-intensive tasks such as compression or hashing. Also, the GIL is always released when doing I/O.

 一些扩展模块, 无论是在标准库还是第三方库里, 在执行计算密集型操作, 比如压缩, 哈希运算时, 会主动释放 GIL; 另在执行 I/O 操作时也会释放 GIL.

<div class="alert alert-danger">
一个常见的误区是: 认为 GIL 会导致 Python 多线程无法利用多核优势; 事实上, 某些精心设计的程序是可以利用多核的
</div>


另因为 GIL 的存在, 在 CPython 中, 大多数 C function 的执行是原子的, 比如 `list.append`; 存在一些第三方库依赖此特性而不需要额外的锁机制来实现线程安全


## Eliminating GIL

Getting rid of the `GIL` is an occasional topic on the `python-dev` mailing list. No one has managed it yet!



## Reference

* [Wiki - Python GIL](https://wiki.python.org/moin/GlobalInterpreterLock)

* [Python 2 - Thread State and the Global Interpreter Lock](https://docs.python.org/2/c-api/init.html#thread-state-and-the-global-interpreter-lock)

* [PEP 311 -- Simplified Global Interpreter Lock Acquisition for Extensions](https://www.python.org/dev/peps/pep-0311/)

* [Understanding the Python GIL](http://www.dabeaz.com/python/UnderstandingGIL.pdf)
