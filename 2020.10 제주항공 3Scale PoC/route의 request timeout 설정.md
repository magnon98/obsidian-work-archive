```
router env에   
    ROUTER_DEFAULT_SERVER_TIMEOUT = 300s
```
 
```
또는 
```
   

```
route의 annotation에   
    haproxy.router.openshift.io/timeout: 300s
```
   

```
$ oc annotate route \<route_name\> \  
    --overwrite haproxy.router.openshift.io/timeout=\<timeout\>\<time_unit\>
```