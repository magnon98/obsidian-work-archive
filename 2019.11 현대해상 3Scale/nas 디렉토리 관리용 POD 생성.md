```
oc adm policy add-scc-to-user anyuid -z default  
oc new-app --name=test --image-stream=java
```
 
```
oc edit dc test  
    spec:  
      containers:  
      - args:  
        - -f  
        - /dev/null  
        command:  
        - /bin/tail  
      securityContext:  
        runAsUser: 0
```
   

```
echo 'apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: nas-root  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 1Gi  
  nfs:  
    path: /nas  
    server: bastion.ocp.bliex.io  
  persistentVolumeReclaimPolicy: Retain  
' | oc create -f -
```
    
```
echo 'apiVersion: v1  
kind: PersistentVolumeClaim  
metadata:  
  name: nas-storage  
spec:  
  accessModes:  
  - ReadWriteOnce  
  resources:  
    requests:  
      storage: 1Gi  
' | oc create -f -
```
   

```
 oc set volume dc/test --add --name=nas -t pvc --claim-name=nas-storage --mount-path=/mnt
```