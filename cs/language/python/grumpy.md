Grumpy
---

Grumpy is a Python to Go source code transcompiler and runtime that is intended to be a near drop-in replacement for CPython 2.7.

The key difference is that it compiles Python source code to Go source code which is then compiled to native code, rather than to bytecode. This means that Grumpy has no VM. The compiled Go source code is a series of calls to the Grumpy runtime, a Go library serving a similar purpose to the Python C API (although the API is incompatible with CPython's).

