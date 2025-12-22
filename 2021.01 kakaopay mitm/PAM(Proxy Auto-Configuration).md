```
[https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_PAC_file](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_PAC_file)
```
    
```
application/x-ns-proxy-autoconfig
```
    
```
function FindProxyForURL(url, host) {  
    if (isPlainHostName(host) || dnsDomainIs(host, ".google.com")) {  
        return "PROXY 192.168.100.151:8080; DIRECT";  
    }  
    else {  
        return "DIRECT";  
    }  
}
```
 
```
$ echo '
```
 
```
listen example-single-static-file  
  bind  *:80  
  mode  http
```
 
```
  timeout connect         5s  
  timeout client          5s  
  timeout server          5s
```
 
```
  monitor-uri /mitm.pac  
  errorfile 200 /etc/haproxy/static/mitm.pac' | sudo tee -a /etc/haproxy/haproxy.cfg
```
   

```
$ sudo mkdir /etc/haproxy/static
```
 
```
$ echo 'HTTP/1.0 200 OK  
Cache-Control: no-cache  
Connection: close  
Content-Type: application/x-ns-proxy-autoconfig
```
 
```
function FindProxyForURL(url, host) {  
    if (isPlainHostName(host) || dnsDomainIs(host, ".google.com")) {  
        return "PROXY 192.168.100.151:8080; DIRECT";  
    }  
    else {  
        return "DIRECT";  
    }  
}' | sudo tee /etc/haproxy/static/mitm.pac
```