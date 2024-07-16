# Temp haproxy waf

Automatically configures an alma8 box to install box to install:  

 * Docker
 * Haproxy 2.8
 * [Modsecurity-spoa](https://github.com/jcmoraisjr/modsecurity-spoa) 0.13
 * Nginx

## Layout

request port 80 <-> haproxy <-> modsecurity spoa <-> nginx  

Haproxy receives a request on port 80, it then sends that request to Docker, which runs a modsecurity container on port 12345. Modsecurity verifies each package using it's ruleset.    
If the request is valid the request is send through nginx, if not, a 403 is given.

## Usage

Logs for haproxy are written to `/var/log/haproxy.log`.  
Logs for modsecurity, use `docker ps` ; docker logs <container id>.  
To provide a test for the waf, use curl 'http://localhost:80/?foo=/etc/passwd&bar=/bin/sh'

