We are given two sequences - a `PUSH` sequence and a `POP` sequence each consisting of `n` integers that are suppose to represent the sequence of values pushed and values popped from a stack, respectively.

We could assume that the stack starts out empty and finishes up empty as well.

The goal is to determine if these sequences could represent valid operation of the stack. In other words, while we are given the order of the values pushed and the order of the values popped, we want to know if there is a way to interleave the push and pop operations to make this the legal behavior of a stack.


First suppose that all values in the sequence are distinct

``` python
def check(en_seq, pop_seq, s):
    """ Suppose that all elements are distinct

    Args:
        en_seq: push sequence
        pop_seq: pop sequence
        s: stack

    Returns:
        true if push and pop sequence are valid, otherwise false
    """
    if not pop_seq:
        return True

    if s and s[-1] == pop_seq[0]:
        s.pop()
        return check(en_seq, pop_seq[1:], s)
    elif not en_seq:
        return False
    else:
        s.append(en_seq[0])
        return check(en_seq[1:], pop_seq, s)
```


Consider the general case, where the values may repeat

``` python
def check_dup(en_seq, pop_seq, s):
    """ The elements in sequence might be duplicate

    Args:
        en_seq: push sequence
        pop_seq: pop sequence
        s: stack

    Returns:
        true if push and pop sequence are valid, otherwise false
    """
    if not pop_seq:
        return True

    def advance():
        if not en_seq:
            return False
        return check_dup(en_seq[1:], pop_seq, s + [en_seq[0]])

    # There are 2 branches when the top element in stack is equal to
    #  the first element in pop sequence
    if s and s[-1] == pop_seq[0]:
        branch1 = check_dup(en_seq, pop_seq[1:], s[:-1])
        if branch1:
            return True
        else:  # branch 2
            return advance()
    else:
        return advance()
```
