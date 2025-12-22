# Template

[https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.2.0.GA/amp/amp.yml](https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.2.0.GA/amp/amp.yml)
   

oc new-app \  
  --file [https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.2.0.GA/amp/amp.yml](https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.2.0.GA/amp/amp.yml) \  
  --param WILDCARD_DOMAIN=apps.doosan.bliex.io
    
# PV
 
apiVersion: v1  
kind: PersistentVolume  
spec:  
accessModes:  
- ReadWriteMany  
capacity:  
storage: 10Gi  
nfs:  
path: /exports/pv0001  
server: nfs  
persistentVolumeReclaimPolicy: Recycle
      

# pv script

```
#!/bin/bash
```
 
```
# Creates PVs on master node
```
 
```
SERVER=nfs  
COUNT=50
```
 
```
oc project default
```
 
```
for i in $(seq 1 $COUNT); do  
   PV=$(cat \<\<EOF  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
 name: pv$(printf %04d $i)  
spec:  
 capacity:  
   storage: 10Gi  
 accessModes:  
   - ReadWriteOnce  
   - ReadWriteMany  
 persistentVolumeReclaimPolicy: Recycle  
 nfs:  
   server: $SERVER  
   path: /exports/pv$(printf %04d $i)  
EOF  
)  
   echo "$PV" | oc create -f -  
done
```
    
# ### 모든 노드에서

$ sudo setsebool -P virt_use_nfs on
       
# pv recycle

$ oc create serviceaccount pv-recycler-controller -n openshift-infra
   

apiVersion: v1  
kind: Pod  
metadata:  
name: pv-recycler-  
namespace: openshift-infra  
spec:  
restartPolicy: Never  
serviceAccount: pv-recycler-controller  
volumes:  
- name: nfsvol  
nfs:  
server: any-server-it-will-be-replaced  
path: any-path-it-will-be-replaced  
containers:  
- name: pv-recycler  
image: "gcr.io/google_containers/busybox"  
command: ["/bin/sh", "-c", "test -e /scrub && rm -rf /scrub/..?* /scrub/.[!.]* /scrub/* && test -z \"$(ls -A /scrub)\" || exit 1"]  
volumeMounts:  
- name: nfsvol  
mountPath: /scrub
      

*(rw,root_squash,sync,no_wdelay)