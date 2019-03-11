Watch
---
All of the read operations in ZooKeeper - `getData()`, `getChildren()`, and `exists()` - have the option of setting a watch as a side effect.

Here is ZooKeeper's definition of a watch: **a watch event is one-time trigger, sent to the client that set the watch, which occurs when the data for which the watch was set changes**.

There are three key points to consider in this definition of a watch:

* One-time trigger

    Watches are one time triggers; if you get a watch event and you want to get notified of future changes, you must set another watch.

    Because watches are one time triggers and there is latency between getting the event and sending a new request to get a watch you cannot reliably see every change that happens to a node in ZooKeeper. Be prepared to handle the case where the `znode` changes multiple times between getting the event and setting the watch again. (You may not care, but at least realize it may happen.)

    There is one case where a watch may be missed: a watch for the existence of a `znode` not yet created will be missed if the `znode` is created and deleted while disconnected.


* Sent to the client

* The data for which the watch was set

    It helps to think of ZooKeeper as maintaining two lists of watches: `data watches` and `child watches`. `getData()` and `exists()` set data watches. `getChildren()` sets child watches.

    Alternatively, it may help to think of watches being set according to the kind of data returned. `getData()` and `exists()` return information about the data of the node, whereas `getChildren()` returns a list of children.


Watches are maintained locally at the ZooKeeper server to which the client is connected.


## What ZooKeeper Guarantees about Watches

With regard to watches, ZooKeeper maintains these guarantees:

* Watches are ordered with respect to other events, other watches, and asynchronous replies. The ZooKeeper client libraries ensures that everything is dispatched in order.

* A client will see a watch event for a znode it is watching before seeing the new data that corresponds to that znode.

* The order of watch events from ZooKeeper corresponds to the order of the updates as seen by the ZooKeeper service.
