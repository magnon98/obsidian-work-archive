### 설치할 3scale 버전 확인
    
### 3scale에 사용할 NFS 확인
    
### 3scale에 사용할 도메인 확인
    
### wildcard domain 활성화여부 체크  
$ oc get dc/router -o yaml | grep WILDCARD -A 1
    
### wildcard domain 활성화  
$ oc project default  
$ oc set env dc/router ROUTER_ALLOW_WILDCARD_ROUTES=true  
$ oc get po
      

### PV 생성
   

#!/bin/bash  
for i in {001..020}; do  
PV=$(cat \<\<EOF  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
name: pv$i  
spec:  
capacity:  
storage: 10Gi  
accessModes:  
- ReadWriteOnce  
- ReadWriteMany  
persistentVolumeReclaimPolicy: Recycle  
nfs:  
server: [NFS 서버 주소]  
path: /exports/pv$i  
EOF  
)  
echo "$PV" | oc create -f -  
done
       
### 3scale 설치  
$ curl [https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.3.0.GA/amp/amp.yml](https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.3.0.GA/amp/amp.yml) -o amp_2.3.0GA.yml
 
$ oc new-project 3scale  
$ oc new-app -f ./amp_2.3.0GA.yml --param WILDCARD_DOMAIN=api.ocp.bliex.io --param WILDCARD_POLICY=Subdomain
 
### PVC 바인딩 확인  
$ oc get pvc
 
### 설치과정 확인  
$ watch oc get po