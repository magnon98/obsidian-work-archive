```
### create namespace  
$ l create ns mitmproxy
```
    
```
### set current namespace  
$ 2022. 3. 16.  config set-context --current --namespace=mitmproxy
```
      

```
### create configmap - mitmproxy-config  
$ echo 'ssl_insecure: true  
allow_hosts:  
- .+\.google.com  
- .+\.bliex.io  
- httpbin.org  
- echo-api.3scale.net  
scripts:  
- /home/mitmproxy/bin/google_apps_header.py' \> config.yaml
```
 
```
$ kubectl create configmap mitmproxy-config --from-file=config.yaml
```
      

```
### create configmap - mitmproxy-script  
$ echo 'from mitmproxy import ctx
```
 
```
def request(flow):  
    #ctx.log.info(f"pretty host: " + flow.request.pretty_host)  
    #ctx.log.info(f"host: " + flow.request.host)
```
 
```
    if flow.request.pretty_host.find("google.com") \> 1:  
        flow.request.headers["X-GoogApps-Allowed-Domains"] = "bliex.com"' \> google_apps_header.py
```
   

```
$ kubectl create configmap mitmproxy-script --from-file=google_apps_header.py
```
       
```
### create deployment - mitmproxy  
$ echo 'apiVersion: apps/v1  
kind: Deployment  
metadata:  
  namespace: mitmproxy  
  name: mitmproxy  
  labels:  
    app: mitmproxy  
spec:  
  selector:  
    matchLabels:  
      app: mitmproxy  
  replicas: 1  
  template:  
    metadata:  
      labels:  
        app: mitmproxy  
    spec:  
      containers:  
      - name: mitm-proxy  
        command:  
        - /home/mitmproxy/bin/mitmdump  
        image: docker-registry.bliex.io:5000/mitmproxy:latest  
        imagePullPolicy: Always  
        ports:  
        - containerPort: 8080  
          name: prx  
          protocol: TCP  
        readinessProbe:  
          failureThreshold: 3  
          periodSeconds: 10  
          successThreshold: 1  
          tcpSocket:  
            port: 8080  
          timeoutSeconds: 1  
        livenessProbe:  
          failureThreshold: 3  
          periodSeconds: 10  
          successThreshold: 1  
          tcpSocket:  
            port: 8080  
          timeoutSeconds: 1  
        resources:  
          limits:  
            cpu: "1"  
            memory: 1Gi  
          requests:  
            cpu: 200m  
            memory: 256Mi  
        startupProbe:  
          failureThreshold: 3  
          periodSeconds: 10  
          successThreshold: 1  
          tcpSocket:  
            port: 8080  
          timeoutSeconds: 1  
        terminationMessagePath: /dev/termination-log  
        terminationMessagePolicy: File  
        volumeMounts:  
        - mountPath: /home/mitmproxy/bin/google_apps_header.py  
          name: script-volume  
          subPath: google_apps_header.py  
        - mountPath: /home/mitmproxy/.mitmproxy/config.yaml  
          name: config-volume  
          subPath: config.yaml  
      dnsPolicy: None  
      dnsConfig:  
        nameservers:  
        - 192.168.100.11  
      volumes:  
      - name: script-volume  
        configMap:  
          name: mitmproxy-script  
          defaultMode: 420  
      - name: config-volume  
        configMap:  
          name: mitmproxy-config  
          defaultMode: 420' \> deployment_mitmproxy.yaml
```
   

```
$ kubectl create -f deployment_mitmproxy.yaml
```
    
```
### create nodeport type service - mitmproxy  
$ kubectl -n mitmproxy expose deployment mitmproxy \  
    --type=NodePort \  
    --name=mitmproxy-nodeport \  
    --labels=app=mitmproxy
```