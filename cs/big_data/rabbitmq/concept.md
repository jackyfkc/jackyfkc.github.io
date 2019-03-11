[Concept](https://www.rabbitmq.com/tutorials/amqp-concepts.html)
----




## Exchange

Exchanges are `matching and routing engines`. They inspect messages and using their binding tables, decides how to forward these messages to message queues.

> Exchange never store messages


## Queue

Message queues are message storage and distribution entities. Each message queue is entirely independent.


## Binding

The relationship between queue and exchange


## Channel
...


## Virtual Host

A collection of exchanges, message queues and associated objects. Virtual hosts are `independent server domains` that share a common authentication and encryption environment.

