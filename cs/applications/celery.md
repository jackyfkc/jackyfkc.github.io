[Celery](http://docs.celeryproject.org/en/latest/getting-started/introduction.html) is a distributed task system.


[Task](http://docs.celeryproject.org/en/latest/userguide/tasks.html)
----

A `task` is a class that can be created out of any callable. It performs dual roles in that it defines both what happens when a task is called (sends a message), and what happens when a worker receives that message.

Every `task` must have a unique name, and a new name will be generated out of the function name if a custom name is not provided.



### [Retry](http://docs.celeryproject.org/en/latest/userguide/tasks.html#retrying)

`app.Task.retry()` can be used to re-execute the task. When you call retry it’ll send a new message, using the same `task-id`, and it’ll take care to make sure the message is delivered to the same queue as the originating task.



[Worker](http://docs.celeryproject.org/en/latest/userguide/workers.html)
---
...

## Time Limits
...


## Rate Limits

Token Bucket...


## Auto scaling
...


Event
-----
The worker has the ability to send a message whenever some event happens. These events are then captured by tools like Flower, and **celery events** to monitor the cluster.



Heartbeat
---
...

* [Django-Celery Connection error?](http://stackoverflow.com/questions/14817181/django-celery-connectionerror-too-many-heartbeats-missed)




[Configuration](http://docs.celeryproject.org/en/latest/userguide/configuration.html)
---
...



[Best Practices](http://docs.celeryproject.org/en/latest/userguide/tasks.html#tips-and-best-practices)
---

## [Optimizing](http://docs.celeryproject.org/en/latest/userguide/optimizing.html)




[FAQ](http://docs.celeryproject.org/en/latest/faq.html)
----

* Why say celery is a distributed task system?



Further Reading
----

* [Celery Documentation](http://docs.celeryproject.org/en/latest/)
