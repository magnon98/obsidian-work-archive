```
[https://docs.mitmproxy.org/stable/concepts-options/](https://docs.mitmproxy.org/stable/concepts-options/)
```
   

```
$ echo 'allow_hosts:  
- .+google.com  
- .+youtube.com  
scripts:  
- /opt/mitm_proxy/script.py' \> ~/.mitmproxy/config.yaml
```
   

```
$ /opt/mitm_proxy/mitmdump
```