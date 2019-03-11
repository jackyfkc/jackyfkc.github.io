Understanding Messaging
---


### Message properties

The `AMQP` protocol defines a set of 14 properties that go with a message. The following are commonly used

* delivery_mode: Marks a message as `persistent` (value of 2) or `transient`

* content_type: Used to describe the `mine-type` of the encoding

* reply_to: Commonly used to name `a callback queue`

* correlation_id: Useful to correlate RPC responses with requests


**Note:** For a message inside Rabbit to _survive a crash_, the message _must_

* Have its `delivery mode` option set to 2(persistent)

* Be published into a `durable` exchange

* Arrive in a `durable` queue



### [Reliability](http://www.rabbitmq.com/reliability.html)

In order to make sure a message is never lost, RabbitMQ supports message acknowledgments.

