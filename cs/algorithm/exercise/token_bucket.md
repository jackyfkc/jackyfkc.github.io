Token Bucket 令牌桶
---
...


Python 源码

``` python
import time


class RateLimiter(object):
    def __init__(self, capacity, per):
        self.capacity = capacity
        self.per = per
        self._rate = capacity / per

        self.last = time.time()
        self.avail = self.capacity

    _time = time.time

    def allow_request(self):
        now = self._time()
        self.avail += (now - self.last) * self._rate
        self.last = now

        if self.avail > self.capacity:
            self.avail = self.capacity

        if self.avail > 1:
            self.avail -= 1
            return True
        return False
```
