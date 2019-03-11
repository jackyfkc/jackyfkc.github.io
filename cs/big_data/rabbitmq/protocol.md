Protocol
---

## Frame Details

**General frame format**

<pre>
0      1         3             7                size+7 size+8
+------+---------+-------------+ +------------+ +-----------+
| type | channel | size        | | payload    | | frame-end |
+------+---------+-------------+ +------------+ +-----------+
 octet     short    long           size octets      octet
</pre>



## Client Architecture

<pre>
          +------------------------+
          |     Application        |
          +-----------+------------+
                      |
          +------------------------+
      +---|       API Layer        |----Client API Layer-----+
      |   +-----------+------------+                         |
      |               |                                      |
      |   +------------------------+    +---------------+    |
      |   |    Connection Manager  +----+ Framing Layer |    |
      |   +-----------+------------+    +---------------+    |
      |               |                                      |
      |   +------------------------+                         |
      +---| Asynchronous I/O Layer |-------------------------+
          +-----------+------------+
                      |
                   -------
           - - - - Network - - - -
                   -------
</pre>

