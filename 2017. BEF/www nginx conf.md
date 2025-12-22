```
$ cat 00_upstreams.conf   
# 00_upstreams.conf
```
 
```
upstream upstream_portal_was {  
server 127.0.0.1:8080;  
}
```
 
```
upstream upstream_grafana {  
server 50.1.111.186:3000;  
}
```
 
```
upstream upstream_apiserver {  
server 50.1.111.187:6443;  
server 50.1.111.188:6443;  
server 50.1.111.189:6443;  
}
```
 
```
upstream upstream_prometheus {  
server 50.1.111.187:30703;  
server 50.1.111.188:30703;  
server 50.1.111.189:30703;  
}
```
 
```
$ cat /etc/nginx/conf.d/00_default_redirect.conf   
# 00_default_redirect.conf
```
 
```
server {  
listen 80 default_server;
```
 
```
server_name _;
```
 
```
return 301 [https://$host$request_uri](https://$host$request_uri);  
}
```
 
```
server {  
    listen 443 default_server;
```
 
```
    server_name _;
```
 
```
    ssl on; 
```
 
```
    ssl_certificate /etc/pki/tls/certs/star_bef_exntu_net.crt;  
    ssl_certificate_key /etc/pki/tls/certs/star_bef_exntu_net.key;
```
 
```
    return 301 [https://www.bef.exntu.net/](https://www.bef.exntu.net/);  
}
```
 
```
$ cat 10_net_exntu_bef_www.conf   
# 10_net_exntu_bef_www.conf
```
 
```
server {  
listen 443 ssl;
```
 
```
server_name [www.bef.exntu.net](http://www.bef.exntu.net);
```
 
```
add_header Cache-Control no-cache;
```
 
```
ssl_certificate /etc/pki/tls/certs/star_bef_exntu_net.crt;  
ssl_certificate_key /etc/pki/tls/certs/star_bef_exntu_net.key;
```
 
```
### portal was  
location /api {  
proxy_pass [http://upstream_portal_was](http://upstream_portal_was);  
}
```
 
```
### Grafana  
location /grafana {  
proxy_pass [http://upstream_grafana](http://upstream_grafana);  
rewrite ^/grafana/(.*)$ /$1 break;  
proxy_set_header  Host $host;  
}
```
 
```
### portal ui  
location / {  
root /usr/share/nginx/html;  
try_files $uri $uri/ $uri/index.html /index.html =404;  
}  
}
```
 
```
$ cat 20_net_exntu_bef_admin.conf   
# 20_net_exntu_bef_admin.conf
```
 
```
server {  
    listen 443 ssl;
```
 
```
    server_name admin.bef.exntu.net;
```
 
```
add_header Cache-Control no-cache;
```
 
```
    ssl_certificate /etc/pki/tls/certs/star_bef_exntu_net.crt;  
    ssl_certificate_key /etc/pki/tls/certs/star_bef_exntu_net.key;
```
 
```
    ### admin console  
    location / {  
        root   /usr/share/nginx/admin;  
        try_files $uri $uri/ $uri/index.html /index.html =404;  
    }  
    ### portal was  
    location /api {  
        proxy_pass [http://upstream_portal_was](http://upstream_portal_was);  
    }  
}
```
 
```
$ cat 30_net_exntu_bef_kube.conf   
# 30_net_exntu_bef_kube.conf  
# rev. proxy for kubernetes api
```
 
```
server {  
listen 6443 ssl;
```
 
```
add_header Cache-Control no-cache;
```
 
```
    server_name kube.bef.exntu.net;
```
 
```
    ssl_certificate /etc/pki/tls/certs/star_bef_exntu_net.crt;  
    ssl_certificate_key /etc/pki/tls/certs/star_bef_exntu_net.key;
```
 
```
### kubernetes master nodes  
location / {  
proxy_pass        [https://upstream_apiserver](https://upstream_apiserver);  
proxy_pass_header Authorization;  
proxy_ssl_name    /etc/pki/tls/certs/apiserver.pem;  
}  
}
```
 
```
$ cat 40_net_exntu_bef_prometheus.conf   
# 40_net_exntu_bef_prometheus.conf
```
 
```
server {  
server_name prometheus.bef.exntu.net;
```
 
```
listen 443 ssl;
```
 
```
    ssl_certificate /etc/pki/tls/certs/star_bef_exntu_net.crt;  
    ssl_certificate_key /etc/pki/tls/certs/star_bef_exntu_net.key;
```
 
```
location / {  
proxy_pass [http://upstream_prometheus](http://upstream_prometheus);  
}  
}
```
 
```
$ cat 99_net_exntu_bef_admin.conf   
# 99_net_exntu_bef_admin.conf
```
 
```
server {  
listen 8888;
```
 
```
add_header Cache-Control no-cache;
```
 
```
### admin ui  
location / {  
root   /usr/share/nginx/admin;  
try_files $uri $uri/ $uri/index.html /index.html =404;  
}
```
 
```
### admin was  
location /api {  
proxy_pass [http://upstream_portal_was](http://upstream_portal_was);  
}  
}
```