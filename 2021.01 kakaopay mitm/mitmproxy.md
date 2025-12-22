```
[https://mitmproxy.org/](https://mitmproxy.org/)  
[https://docs.mitmproxy.org/stable/](https://docs.mitmproxy.org/stable/)  
[https://hub.docker.com/r/mitmproxy/mitmproxy](https://hub.docker.com/r/mitmproxy/mitmproxy)  
[http://mitm.it/](http://mitm.it/)  
[https://docs.mitmproxy.org/stable/addons-examples/#scripting-minimal-example](https://docs.mitmproxy.org/stable/addons-examples/#scripting-minimal-example)
```
    
```
### 설정
```
 
```
$ sudo mkdir /opt/mitm_proxy  
$ sudo chown bliex:bliex /opt/mitm_proxy  
$ curl [https://snapshots.mitmproxy.org/6.0.2/mitmproxy-6.0.2-linux.tar.gz](https://snapshots.mitmproxy.org/6.0.2/mitmproxy-6.0.2-linux.tar.gz) | tar zxf - -C /opt/mitm_proxy
```
 
```
$ echo '  
def request(flow):  
    if flow.request.pretty_host.index("3scale.net") \> 1:  
        flow.request.headers["X-GoogApps-Allowed-Domains"] = "3scale.net"  
' \> /opt/mitm_proxy/script.py
```
   

```
$ /opt/mitm_proxy/mitmproxy -s /opt/mitm_proxy/script.py
```
    
```
### 테스트  
$ HTTPS_PROXY=http://localhost:8080 curl -k [https://echo-api.3scale.net/](https://echo-api.3scale.net/) 
```
    
```
c:\\> curl -k [https://echo-api.3scale.net/](https://echo-api.3scale.net/) --proxy [http://localhost:8080](http://localhost:8080)
```
    
```
### 인증서 사용한 곳에 접속  
접속시 502 bad gateway 에러.  
-k 옵션을 쓰면 접속 가능하지만, 잠긴 열쇠로 표시됨.
```

```
docker run --rm -it \  
    -v ~/.mitmproxy:/home/mitmproxy/.mitmproxy \  
    -p 8080:8080 \  
    -p 8081:8081 \  
    mitmproxy/mitmproxy mitmweb \  
    --web-host 0.0.0.0
```

```
### ***.google.com ***.youtube.com 도메인은 처리 안하고 passthrough.  
$ /opt/mitm_proxy/mitmdump \  
    --ignore-hosts '(?\<!google\.com)$' \  
    --ignore-hosts '(?\<!youtube\.com)$'
```
    
```
### ***.google.com ***.youtube.com 도메인만 처리하고 나머지만 passthrough  
$ /opt/mitm_proxy/mitmdump \  
    --allow-hosts '.+google.com' \  
    --allow-hosts '.+youtube.com'
```
   

```
-H '/X-GoogApps-Allowed-Domains/bliex.com'
```