```
    spec:  
      initContainers:  
      - name: volume-mount-hack  
        image: alpine:3.7  
        command:  
        - sh  
        - -c  
        - 'chmod -R a+rwx /var/lib/grafana'  
        volumeMounts:  
        - name: pvc-akamai-ui-dev  
          mountPath: /var/lib/grafana
```

```
grafana-cli plugins install grafana-simple-json-datasource  
grafana-cli plugins install simpod-json-datasource
```