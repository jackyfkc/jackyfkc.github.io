logging
----

## Anatomy
...

### Critical Data Structures

* Logger

    logging channel

* Manager

    There is just one instance, which holds the hierarchy of loggers

* Handler

    dispatch logging events to specific destination



### Global States

``` python
root = RootLogger(WARNING)
Logger.root = root
Logger.manager = Manager(Logger.root)


def getLogger(name=None):
    """
    Return a logger with the specified name, creating it if necessary.

    If no name is specified, return the root logger.
    """
    if name:
        return Logger.manager.getLogger(name)
    else:
        return root
```
