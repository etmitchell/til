#Apache

While working on a side project we realized we would need to forward API requests (HTTP) from one server to another. 
We would use the main server with the domain name attached as the domain for our REST API endpoint and forward (actually, we proxied) the requests to another server. 
Here is our setup:

Server A is running Apache in AWS and Server B is running Flask on port XXXX. We would like GET requests coming into our API to go through servera.io and redirect to our serverb.io.
This was achieved through the use of the mod_proxy module in Apache. Adding the following line to your http.conf will redirect all traffic to your destination server: 

ProxyPass    /api/    http://serverb.io/api/

It's as simple as that.

Using RedirectMatch on a regex worked, kinda, but as part of the spec for Apache and for HTTP it returned a 301 status which makes for an icky API. 
