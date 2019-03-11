RabbitMQ
---

[RabbitMQ](https://www.rabbitmq.com) is a messaging broker. It gives your application a common platform to send and receive messages.


**Overall AMQ model**

<pre>

                                    Server
                        +----------------------------+
                        |        Virtual host        |
                        |    +-------------------+   |
                        |    |      Exchange     |   |
   +-------------+      |    |      +-------+    |   |
   | Publisher   |    ---------->   |       |    |   |
   | application |      |    |      +---+---+    |   |
   +-------------+      |    |          |        |   |
                        |    |       Message     |   |
                        |    |        Queue      |   |
   +-------------+      |    |      +-------+    |   |
   |  Consumer   |   <-----------   +-------+    |   |
   | application |      |    |      +-------+    |   |
   +-------------+      |    |      +-------+    |   |
                        |    +-------------------+   |
                        +----------------------------+

</pre>

- - -

* [Concept](concept.md)

* [Broker](broker.md)

* [Consumer](consumer.md)

* [Cluster](cluster.md)

- - -

* [Protocol](protocol.md)



## Further Readings

* [Some queuing theory: throughput, latency and bandwidth](https://www.rabbitmq.com/blog/2012/05/11/some-queuing-theory-throughput-latency-and-bandwidth/)

* [RabbitMQ Performance Measurement - Part I](https://www.rabbitmq.com/blog/2012/04/17/rabbitmq-performance-measurements-part-1/)

* [RabbitMQ Performance Measurement - Part 2](https://www.rabbitmq.com/blog/2012/04/25/rabbitmq-performance-measurements-part-2/)


* [Advanced Message Queuing Protocol - Protocol Specification](https://www.rabbitmq.com/resources/specs/amqp0-9-1.pdf)

* RabbitMQ in Action

* [Very fast and scalable topic routing](http://www.rabbitmq.com/blog/2010/09/14/very-fast-and-scalable-topic-routing-part-1/)

* [RabbitMQ Blog](https://www.rabbitmq.com/blog/)

* [RabbitMQ Hits One Million Messages Per Second on Google Compute Engine](https://blog.pivotal.io/pivotal/products/rabbitmq-hits-one-million-messages-per-second-on-google-compute-engine)
