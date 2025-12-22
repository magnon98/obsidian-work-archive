```
$ oc rsh -c system-provider system-app-6-xxxxx \  
    cat /opt/system/app/views/provider/sessions/new.html.slim \  
    | tr -d '\r' \  
    | sed 's/enforceSSO: false/enforceSSO: true/' \  
    \> new.html.slim
```
 
```
$ oc create configmap new-html-slim --from-file=new.html.slim
```
 
```
$ oc set volume dc/system-app \  
    -c system-provider \  
    --add \  
    --name=new-html-slim \  
    --mount-path /opt/system/app/views/provider/sessions/new.html.slim \  
    --sub-path new.html.slim \  
    --source='{"configMap":{"name":"new-html-slim","items":[{"key":"new.html.slim","path":"new.html.slim"}]}}'
```