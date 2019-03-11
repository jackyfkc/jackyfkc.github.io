Lock Free
---
...


## A non-blocking Stack

Non-blocking stack using Treiber's algorithm

``` java
public class ConcurrentStack<E> {
    private AtomicReference<Node<E>> head = new AtomicReference<>();

    public void push(E value) {
        Node<E> newNode = new Node<E>(value);

        while (true) {
            Node<E> curHead = this.head.get();
            newNode.next = curHead;

            if (this.head.compareAndSet(curHead, newNode))
                break;
        }
    }

    public E pop() {
        while (true) {
            Node<E> curHead = this.head.get();
            if (curHead == null)
                return null;

            Node<E> next = curHead.next;
            if (this.head.compareAndSet(curHead, next))
                return curHead.value;
        }
    }

    private static class Node<E> {
        final E value;
        Node<E> next;

        Node(E value) {
            this.value = value;
        }
    }
}
```

CAS enables atomic conditional updates on a single pointer, but not on two. So to construct a non-blocking linked list, tree, or hash table, we need to find a way to update multiple pointers with CAS without leaving the data structure in an inconsistent state


The "trick" to building non-blocking algorithms for nontrivial data structures is to

* make sure that the data structure is always in a consistent state, even between the time that a thread starts modifying the data structure and the time it finishes, and to

* make sure that other threads can tell not only whether the first thread has finished its update or is still in the middle of it, but also what operations would be required to complete the update if the first thread went AWOL.

构建非阻塞版本的复杂数据结构的关键技巧是保证数据结构总是处于一致状态中, 即使是某个线程在开始修改到操作完成之间. 并且确保其它线程不仅可以区分出第一个线程已经完成操作还是正处于操作之中, 还应该 知道如果第一个线程故障了, 应该如何继续完成后续操作.


If a thread arrives on the scene to find the data structure in the middle of an update, it can "help" the thread already performing the update by finishing the update for it, and then proceeding with its own operation. When the first thread gets around to trying to finish its own update, it will realize that the work is no longer necessary and just return because the CAS will detect the interference (in this case, constructive interference) from the helping thread.


This **help thy neighbor** requirement is needed to make the data structure resistant to the failure of individual threads. If a thread arrived to find the data structure in mid-update by another thread and just waited until that thread finished its update, it could wait forever if the other thread fails in the middle of its operation. Even in the absence of failure, this approach would offer poor performance because the newly arriving thread would have to yield the processor, incurring a context switch, or wait for its quantum to expire, which is even worse.


## A non-blocking Queue

Michael-Scott non-blocking queue algorithm

...
