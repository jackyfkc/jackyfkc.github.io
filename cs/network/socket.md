writing...


> Socket 套接字就只是一个概念而已, 并不存在实体 (硬件), 如果一定要赋予它一个实体, 我们可以说那些控制信息就是套接字的实体, 或者说存放控制信息的内存空间就是套接字的实体

By default, all sockets are blocking.

默认情况下, 所有的套接字都是阻塞的.


IO Model
---

### blocking I/O 阻塞 I/O
...


### non-blocking I/O 非阻塞 I/O
...


### I/O multiplexing  多路复用
...


Socket Option 套接字选项
---

The most commonly used options are `SO_KEEPALIVE`, `SO_RCVBUF`, `SO_SNDBUF`, and `SO_REUSEADDR`.

Every TCP socket has a `send buffer` and a `receiver buffer`, and every UDP socket has a `receive buffer`. The `SO_SNDBUF` and `SO_RCVBUF` socket options let us change the sizes of these buffers.


```python

# An example to limit receive buffer length and send buffer length

import socket

sock = socket.socket()

sock.getsockopt(socket.SOL_SOCKET, socket.SO_SNDBUF)
sock.getsockopt(socket.SOL_SOCKET, socket.SO_RCVBUF)
```



Further Reading
---

* Unix Network Programming
