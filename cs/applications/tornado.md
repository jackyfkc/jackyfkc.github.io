Tornado is a Python web framework and asynchronous networking library, originally developed at FriendFeed; ideal for `long polling`, `WebSockets`, and other applications that require a long-lived connection to each user.

Tornado 是一个 Python Web 框架, 同时也是一个异步网络库. Tornado 适用于 `Long polling`, `WebSockets` 以及需要长连接的场景.


Tornado can be roughly divided into four major components:

* A web framework (including `RequestHandler` which is sub-classed to create web applications, and various supporting classes).

* Client- and server-side implementations of HTTP (`HTTPServer` and `AsyncHTTPClient`).

* An asynchronous networking library including the classes `IOLoop` and `IOStream`, which serve as the building blocks for the HTTP components and can also be used to implement other protocols.

* A coroutine library (`tornado.gen`) which allows asynchronous code to be written in a more straightforward way than chaining callbacks.


Anatomy
---
To minimize the cost of concurrent connections, Tornado uses a `single-threaded event loop`.

...


Concept
----

* [Asynchronous](https://tornado.readthedocs.io/en/stable/guide/async.html)

There are many styles of asynchronous interfaces

* Callback argument

* Return a placeholder (Future, Promise, Deferred)

* Deliver to a queue

* Callback registry (e.g. POSIX signals)


### [Coroutine](http://www.tornadoweb.org/en/stable/guide/coroutines.html)

Coroutines are the recommended way to write asynchronous code in Tornado. Coroutines use the Python `yield` keyword to suspend and resume execution instead of a chain of callbacks


Here is a highly simplified version of the coroutine decorator’s inner loop

``` python
# Simplified inner loop of tornado.gen.Runner

def run(self):
    # send(x) makes the current yield return x.
    # It returns when the next yield is reached

    future = self.gen.send(self.next)

    def callback(f):
        self.next = f.result()
        self.run()

    future.add_done_callback(callback)
```


Changelog In Github
---

* [Lockless implementation of add_callback](https://github.com/tornadoweb/tornado/pull/1876)


[FAQ](http://www.tornadoweb.org/en/stable/faq.html)
---

* [Why StackContext?](http://www.tornadoweb.org/en/stable/stack_context.html)

