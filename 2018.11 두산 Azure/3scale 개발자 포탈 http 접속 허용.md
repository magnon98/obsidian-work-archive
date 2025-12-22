```
$ oc rsh -c system-developer -t system-app-1-tchsz  cat config/settings.yml \> settings.yml  
$ oc create configmap system-developer-ssl-config --from-file=./settings.yml  
$ oc set volume dc/system-app --add --name=developer-ssl-config \  
  --mount-path /opt/system/config/settings.yml \  
  --sub-path settings.yml \  
  --source='{"configMap":{"name":"system-developer-ssl-config","items":[{"key":"settings.yml","path":"settings.yml"}]}}'
```