Hystrix is a latency and fault tolerance library designed to isolate points of access to remote systems, services and 3rd party libraries, stop cascading failure and enable resilience in complex distributed systems where failure is inevitable.


What is Hystrix for
---
Hystrix is designed to do the following:

* Give protection from and control over latency and failure from dependencies accessed (typically over the network) via third-party client libraries.

* Stop cascading failures in a complex distributed system.

* Fail fast and rapidly recover.

* Fallback and gracefully degrade when possible.

* Enable near real-time monitoring, alerting, and operational control.


### How Does Hystrix Accomplish Its Goals?


Hystrix does this by:

* Wrapping all calls to external systems (or “dependencies”) in a `HystrixCommand` or `HystrixObservableCommand` object which typically executes within a separate thread (this is an example of the command pattern).

* Timing-out calls that take longer than thresholds you define. There is a default, but for most dependencies you custom-set these timeouts by means of “properties” so that they are slightly higher than the measured 99.5th percentile performance for each dependency.

* Maintaining a small thread-pool (or semaphore) for each dependency; if it becomes full, requests destined for that dependency will be immediately rejected instead of queued up.

* Measuring successes, failures (exceptions thrown by client), timeouts, and thread rejections.

* Tripping a circuit-breaker to stop all requests to a particular service for a period of time, either manually or automatically if the error percentage for the service passes a threshold.

* Performing fallback logic when a request fails, is rejected, times-out, or short-circuits.

* Monitoring metrics and configuration changes in near real-time.


Further Reading
---

* [Hystrix - How To Use](https://github.com/Netflix/Hystrix/wiki/How-To-Use)

* [Hystrix - How it Works](https://github.com/Netflix/Hystrix/wiki/How-it-Works)
