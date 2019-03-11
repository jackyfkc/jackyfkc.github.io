Nginx Load Balancing
---

There are both software and hardware load balancers and nginx has the ability to run as a software load balancer using the `http_proxy` module.


## Overview

Load balancing across multiple application instances is a commonly used technique for optimizing resource utilization, maximizing throughput, and ensuring fault-tolerant configurations.


To start using NGINX with a group of servers, first, you need to define the group with the `upstream` directive. The directive is placed in the `http` context.

Servers in the group are configured using the `server` directive

```
http {
    upstream backend {
        server backend1.example.com weight=5;
        server backend2.example.com;
        server 192.0.0.1 backup;
    }
}
```

To pass requests to a server group, the name of the group is specified in the proxy_pass directive (or `fastcgi_pass`, `memcached_pass`, `uwsgi_pass`, `scgi_pass` depending on the protocol). In the below example, a virtual server running on NGINX passes all requests to the backend server group defined in the previous example:

```
server {
    location / {
        proxy_pass http://backend;
    }
}
```


## Load Balancing Method

NGINX supports four load balancing methods


### Round-robin

Requests are distributed evenly across the servers with `server weights` taken into consideration. This method is used by default (there is no directive for enabling it):

```
upstream backend {
   server backend1.example.com;
   server backend2.example.com;
}
```

### least_conn

A request is sent to the server with the least number of active connections with `server weights` taken into consideration:

```
upstream backend {
    least_conn;

    server backend1.example.com;
    server backend2.example.com;
}
```

### ip_hash

The server to which a request is sent is determined from the client IP address. In this case, either the first three octets of IPv4 address or the whole IPv6 address are used to calculate the hash value. The method guarantees that requests from the same address get to the same server unless it is not available.

```
upstream backend {
    ip_hash;

    server backend1.example.com;
    server backend2.example.com;
}
```

If one of the servers needs to be temporarily removed, it can be marked with the `down` parameter in order to preserve the current hashing of client IP addresses. Requests that were to be processed by this server are automatically sent to the next server in the group:

```
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com down;
}
```

### Generic hash

The server to which a request is sent is determined from a user-defined key which may be a text, variable, or their combination. For example, the key may be a source IP and port, or URI:

```
upstream backend {
    hash $request_uri consistent;

    server backend1.example.com;
    server backend2.example.com;
}
```

The optional consistent parameter to the `hash` directive enables `ketama` consistent hash load balancing. Requests will be evenly distributed across all upstream servers based on the user-defined hashed key value. If an upstream server is added to or removed from an upstream group, only few keys will be remapped which will minimize cache misses in case of load balancing cache servers and other applications that accumulate state.


## Server Weights

By default, NGINX distributes requests among the servers in the group according to their weights using the round-robin method. The `weight` parameter of the `server` directive sets the weight of a server, by default, it is 1:

```
upstream backend {
    server backend1.example.com weight=5;
    server backend2.example.com;
    server 192.0.0.1 backup;
}
```

In the example, **backend1.example.com** has weight 5; the other two servers have the default weight (1), but the one with IP address 192.0.0.1 is marked as a backup server and does not receive requests unless both of the other servers are unavailable. With this configuration of weights, out of every six requests, five are sent **backend1.example.com** and one to **backend2.example.com**.


## Passive Health Monitoring

When NGINX considers a server unavailable, it temporarily stops sending requests to that server until it is considered active again. The following parameters of the server directive configure the conditions to consider a server unavailable:

* The `fail_timeout` parameter sets the time during which the specified number of failed attempts should happen and still consider the server unavailable. In other words, the server is unavailable for the interval set by `fail_timeout`.

* The `max_fails` parameter sets the number of failed attempts that should happen during the specified time to still consider the server unavailable.

The default values are 10 seconds and 1 attempt. So if NGINX fails to send a request to some server or does not receive a response from this server at least once, it immediately considers the server unavailable for 10 seconds. The following example shows how to set these parameters:

```
upstream backend {
    server backend1.example.com;
    server backend2.example.com max_fails=3 fail_timeout=30s;
    server backend3.example.com max_fails=2;
}
```


## References

* [nginx load balancing – http load balancer](https://www.nginx.com/resources/admin-guide/load-balancer/)

