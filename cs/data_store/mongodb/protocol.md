[Wire Protocol](https://docs.mongodb.com/manual/reference/mongodb-wire-protocol/)
---

MongoDB wire protocol is `socket` based, `request-response style` protocol. Clients communicate with the database serve through a regular TCP/IP socket, without connection handshake.


**Standard Message Header**

``` c
struct MsgHeader {
    int32   messageLength; // total message size, including this
    int32   requestID;     // identifier for this message
    int32   responseTo;    // requestID from the original request
                           //   (used in responses from db)
    int32   opCode;        // request type - see table below
}
```