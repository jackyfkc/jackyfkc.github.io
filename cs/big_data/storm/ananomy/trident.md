[Trident](http://storm.apache.org/releases/1.0.2/Trident-tutorial.html)
---

Trident is a high-level abstraction for doing real-time computing on top of Storm. Trident adds primitives for doing `stateful`, `incremental` processing on top of any database or persistence store.

Trident has consistent, exactly-once semantics.


<div class="alert alert-info"> A key problem to solve with real-time computation is how to manage state so that updates are idempotent in the face of failures and retries.
</div>

Trident solves this problem by doing two things:

* Each batch is given a unique id called the `transaction id`. If a batch is retried it will have the exact same transaction id.

* State updates are ordered among batches. That is, the state updates for batch 3 won't be applied until the state updates for batch 2 have succeeded.

