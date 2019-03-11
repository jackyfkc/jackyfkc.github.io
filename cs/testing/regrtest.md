attribute.py
------------

```python
class Attribute(object):
    """
    To simulate `attribute` in C#
    """
    def __call__(self, f):
        try:
            f._attributes.append(self)
        except:
            f._attributes = [self]
        return f


class ID(Attribute):
    """
    Unique identifier of the test
    """
    def __init__(self, id):
        self._id = id

    @property
    def Id(self):
        return self._id


class Tags(Attribute):
    """
    Tags are an optional method of describing additional metadata about the test.
    """
    def __init__(self, name):
        self._name = name

    @property
    def Name(self):
        return self._name


class TestCategory(Attribute):
    """
    Class used to specify the category of a unit test
    """
    def __init__(self, name):
        self._name = name
    
    @property
    def Name(self):
        return self._name


class Priority(Attribute):
    """
    Used to specify the priority of a unit test
    """
    def __init(self, priority):
        self._priority = priority

    @property
    def Priority(self):
        return self._priority

"""
Class Decorator
"""
def TestTarget(name):
    def wrapper(original_class):
        original_class._test_target = name
        return original_class
    return wrapper


"""
Helper Routines
"""
   
class AmbiguousMatchError(Exception):
    # More than one of the requested attributes was found
    pass


class ArgumentNullError(Exception):
    pass

   
def get_custom_attributes(func):
    """
    Retrieves a list of the custom attributes applied to a function
    """
    return func._attributes or []


def get_custom_attribute(func, attr_type):
    """
    Retrieves a custom attribute applied to a function. Parameters specify the
    function, and the type of the custom attribute to search for.
    """
    if func is None or attr_type is None:
        raise ArgumentNullError('func or attr_type is null')

    if not issubclass(attr_type, Attribute):
        raise TypeError('attr_type is not derived from Attribute')

    try:
        func._attributes
    except AttributeError:
        return None

    attrs = [attr for attr in func._attributes if isinstance(attr, attr_type)]
    if len(attrs) > 1:
        raise AmbiguousMatchError()    
    return attrs[0] if len(attrs) == 1 else None
```


