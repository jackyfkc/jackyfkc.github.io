subprocess
---

In linux, subprocess is implemented with `fork` + `exec`



## An example

Here is an example to show how a process capture its child's standard output, see more details in [How to capture python subprocess stdout in unittest
](https://stackoverflow.com/questions/47066063/how-to-capture-python-subprocess-stdout-in-unittest/47066898#47066898)


``` python
import os
import subprocess

from contextlib import contextmanager


@contextmanager
def redirect_stdout(new_out):
    old_stdout = os.dup(1)
    try:
        os.dup2(new_out, 1)
        yield
    finally:
        os.dup2(old_stdout, 1)


def test():
    reader, writer = os.pipe()

    with redirect_stdout(writer):
        subprocess.call(['/bin/echo', 'something happened'], shell=False)

    print(os.read(reader, 1024))
```
