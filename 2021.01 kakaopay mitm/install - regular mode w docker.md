```
### ============================================================================  
### install mitmproxy on VM  
### ============================================================================
```
   

```
$ sudo hostnamectl set-hostname mitmproxy-docker
```
 
```
$ sudo mkdir /opt/mitmproxy  
$ sudo chown bliex:bliex /opt/mitmproxy  
$ curl [https://snapshots.mitmproxy.org/6.0.2/mitmproxy-6.0.2-linux.tar.gz](https://snapshots.mitmproxy.org/6.0.2/mitmproxy-6.0.2-linux.tar.gz) | tar zxf - -C /opt/mitmproxy
```
   

```
$ echo 'def request(flow):  
    if flow.request.pretty_host.index("google.com") \> 1:  
        flow.request.headers["X-GoogApps-Allowed-Domains"] = "kakaocorp.com"  
' \> /opt/mitmproxy/script.py
```
      

```
$ /opt/mitmproxy/mitmdump -s /opt/mitmproxy/script.py
```
    
```
$ echo 'allow_hosts:  
- .+google.com  
scripts:  
- /opt/mitmproxy/script.py' \> ~/.mitmproxy/config.yaml
```
   

```
$ /opt/mitmproxy/mitmdump
```
   

```
### [http://mitm.it/](http://mitm.it/)
```
       
```
### ============================================================================  
### install docker  
### ============================================================================
```
    
```
$ sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release  
$ curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://download.docker.com/linux/ubuntu/gpg) | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
 
```
$ echo \  
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] [https://download.docker.com/linux/ubuntu](https://download.docker.com/linux/ubuntu) \  
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list \> /dev/null
```
 
```
$ sudo apt update  
$ sudo apt install docker-ce docker-ce-cli containerd.io
```
 
```
$ systemctl status docker  
$ sudo usermod -aG docker bliex
```
          
```
### ============================================================================  
### install mitmproxy on docker  
### ============================================================================
```
      

```
$ sudo mkdir -p /opt/mitmproxy-docker/bin  
$ sudo chown -R bliex:bliex /opt/mitmproxy-docker
```
 
```
$ cp /opt/mitmproxy/mitmdump /opt/mitmproxy-docker/bin/
```
    
```
$ echo 'def request(flow):  
    if flow.request.pretty_host.endswith("google.com"):  
        flow.request.headers["X-GoogApps-Allowed-Domains"] = "bliex.com"  
' \> /opt/mitmproxy-docker/bin/google_apps_header.py
```
 
```
$ cp -r ~/.mitmproxy ./  
$ echo 'allow_hosts:  
- .+google.com  
scripts:  
- /home/mitmproxy/bin/google_apps_header.py' \> /opt/mitmproxy-docker/.mitmproxy/config.yaml
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
ADD --chown=mitmproxy:mitmproxy ./.mitmproxy /home/mitmproxy/.mitmproxy/
```
 
```
EXPOSE 8080/tcp
```
 
```
USER mitmproxy
```
 
```
ENTRYPOINT ["/home/mitmproxy/bin/mitmdump", "--mode", "transparent"]' \> Dockerfile
```
   

```
$ docker build . -t mitmproxy
```
    
```
$ for i in {01..05}; do docker run -d -restart=unless-stopped -p 188$i:8080 --name mitm$i mitmproxy; done
```
         

```
### ============================================================================  
### install haproxy  
### ============================================================================
```
   

```
$ sudo apt install haproxy  
$ systemctl status haproxy
```
    
```
$ sudo vi /etc/haproxy/haproxy.cfg
```
 
```
global  
  log /dev/log  local0  
  log /dev/log  local1 notice  
  chroot /var/lib/haproxy  
  stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners  
  stats timeout 30s  
  user haproxy  
  group haproxy  
  daemon
```
 
```
listen tcp-in  
  balance roundrobin  
  #balance leastconn  
  #balance source
```
 
```
  bind *:8080  
  log global  
  mode tcp  
  option tcplog
```
 
```
  timeout connect         5s  
  timeout client          5s  
  timeout server          5s  
  timeout check           1s
```
 
```
  server mitm01 localhost:18801 check  
  server mitm02 localhost:18802 check  
  server mitm03 localhost:18803 check  
  server mitm04 localhost:18804 check  
  server mitm05 localhost:18805 check  
  server mitm06 localhost:18806 check  
  server mitm07 localhost:18807 check  
  server mitm08 localhost:18808 check  
  server mitm09 localhost:18809 check
```
      

```
$ sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg -c
```
 
```
$ sudo systemctl restart haproxy
```
         

```
### ============================================================================  
###   
### ============================================================================
```