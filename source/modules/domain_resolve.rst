
.. meta::
   :description: The Upstream Domain Resolve module implements a load balancer that resolves an upstream domain name asynchronously.

Upstream Domain Resolve
=======================

Description
-----------
**ngx_upstream_jdomain** - a load-balancer that resolves an upstream domain name asynchronously. It chooses one IP from its buffer according to round-robin for each request. Its buffer has the latest IPs of the backend domain name. At every interval (one second by default), it resolves the domain name. If it fails to resolve the domain name, the buffer retains the last successfully resolved IPs.

Example
^^^^^^^

.. code-block:: nginx

  http {
          resolver 8.8.8.8;
          resolver_timeout 10s;
      
          upstream backend {
                  jdomain  www.baidu.com;
                  #keepalive 10;
         }
    server {
      listen       8080;   

      location / {
        proxy_pass http://backend;
      }       
   }
  }
  
  

Directives
----------

jdomain
^^^^^^^
:Syntax: *jdomain <domain-name> [port] [max_ips] [retry_off]*
:Default: *none 80 1 20*
:Context: *upstream*

:``port``: Backend's listening port.
:``max_ips``: IP buffer size.
:``retry_off``: Do not retry if one IP fails.



Installtion
-----------
:github:`Download <wdaike/ngx_upstream_jdomain>` the module.

.. code-block:: bash

  --add-module=<path>



Authors
-------
Questions/patches to wdaike<wdaike@163.com>, Baidu Inc.
