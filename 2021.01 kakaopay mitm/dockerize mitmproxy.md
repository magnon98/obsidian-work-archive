```
base image  
: registry.access.redhat.com/ubi8/ubi-minimal
```
 
```
install docker on centos  
: [https://docs.docker.com/engine/install/centos/](https://docs.docker.com/engine/install/centos/)
```
       
```
$ mkdir bin  
$ curl [https://snapshots.mitmproxy.org/6.0.2/mitmproxy-6.0.2-linux.tar.gz](https://snapshots.mitmproxy.org/6.0.2/mitmproxy-6.0.2-linux.tar.gz) | tar zxf - -C ./bin  
$ cp ~/.mitmproxy ./certs
```
   

```
$ echo 'FROM registry.access.redhat.com/ubi8/ubi
```
 
```
RUN useradd mitmproxy && \  
    mkdir /home/mitmproxy/.mitmproxy /home/mitmproxy/bin && \  
    chown mitmproxy:mitmproxy /home/mitmproxy/.mitmproxy /home/mitmproxy/bin
```
   

```
ADD --chown=mitmproxy:mitmproxy ./bin /home/mitmproxy/bin/  
ADD --chown=mitmproxy:mitmproxy ./certs /home/mitmproxy/.mitmproxy/
```
 
```
EXPOSE 8080/tcp
```
 
```
USER mitmproxy
```
 
```
ENTRYPOINT ["/home/mitmproxy/bin/mitmdump", "-s", "/home/mitmproxy/bin/google_apps_header.py"]' \> Dockerfile
```
    
```
$ sudo docker build . -t mitmproxy
```
 
```
$ docker run --rm -p 8080:8080 mitm_proxy  --allow-hosts '.+3scale\.net'
```