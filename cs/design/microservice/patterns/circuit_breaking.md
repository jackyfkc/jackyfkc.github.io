Circuit Breaking
---
Circuit breaking is a critical component of distributed systems. It’s nearly always better to fail quickly and apply back pressure downstream as soon as possible.


The Circuit Breaker pattern, popularized by _Michael Nygard_ in his book, _Release It!_, can prevent an application from repeatedly trying to execute an operation that's likely to fail. Allowing it to continue without waiting for the fault to be fixed or wasting CPU cycles while it determines that the fault is long lasting.

The Circuit Breaker pattern also enables an application to detect whether the fault has been resolved. If the problem appears to have been fixed, the application can try to invoke the operation.


<div class="alert alert-info">
The purpose of the Circuit Breaker pattern is different than the Retry pattern. The Retry pattern enables an application to retry an operation in the expectation that it'll succeed. The Circuit Breaker pattern prevents an application from performing an operation that is likely to fail. An application can combine these two patterns by using the Retry pattern to invoke an operation through a circuit breaker. However, the retry logic should be sensitive to any exceptions returned by the circuit breaker and abandon retry attempts if the circuit breaker indicates that a fault is not transient.
</div>


### When to use this pattern

* To prevent an application from trying to invoke a remote service or access a shared resource if this operation is highly likely to fail.



Further Reading
---

* [Hystrix](https://github.com/Netflix/Hystrix/wiki/How-it-Works#circuit-breaker)

    Hystrix is no longer maintained, use Resilience4J intead

* [Circuit Breaker Pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker)
