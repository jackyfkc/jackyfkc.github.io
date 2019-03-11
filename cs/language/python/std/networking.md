Web + Networking
---



## CGI

When a web server receives a request for a CGI script, it simply executes the scripts directly(Fork/Exec) and returns the output to the browser.

<pre>
    +-------------+        +--------------+
    | Web Server  | -----> | CGI Program  |
    +-------------+        +--------------+
</pre>

The CGI script retrieve things like the Request URI, client IP Address or Server Host from `environment variables`.


## FastCGI

FastCGI is a direct replacement for CGI. Instead of the web server talking to the program directly, the web server talks to a FastCGI server instead. The FastCGI server is another daemon/background program, running on the computer, that handles the task of running the desired script.

<pre>
                                         +------------+
                                         | CGI Program|
                                         +------------+
                                        /
    +-------------+      +---------+   / +------------+
    | Web Server  | ---> | FastCGI | ->  |CGI Program |
    |             |      | Server  |   \ +------------+
    +-------------+      +---------+    \
                                         +------------+
                                         |CGI Program |
                                         +------------+
</pre>

The FastCGI server is typically long running, so it does not need to fork itself for each request, and can typically handle many connections.


## WSGI

* [PEP 333 -- Python Web Server Gateway Interface v1.0](https://www.python.org/dev/peps/pep-0333/)




