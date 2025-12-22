PersistentVolume 준비  
AMP 설치시 PVC를 이용해 마운트를 하는 부분이 있어 PV를 미리 준비해야 함.  
여기서는 DNS 서버에 NFS 서버 설정을 한 뒤 NAS로 사용함.  
   
**각** **노드에서** **NFS** **마운트**  

```
$ sudo mkdir /opt/pv
$ sudo mount 192.168.100.40:/nas_data/pv /opt/pv
$ echo "192.168.100.40:/nas_data/pv /opt/pv       nfs    defaults        0 0" | sudo tee -a /etc/fstab
```
    
**마스터** **노드에서** **PV** **생성**  
`### PV` 생성에 사용할 `YAML` 파일 준비  

```
$ cat \<\<EOF \> pv.yml
---
apiVersion: v1
kind: Template
metadata:
  creationTimestamp: null
  name: "system"
objects:
- apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: pv\${PV}
  spec:
    accessModes:
    - ReadWriteOnce
    - ReadWriteMany
    capacity:
      storage: 1Gi
    persistentVolumeReclaimPolicy: Recycle
    hostPath:
      path: \${PATH}/\${PV}
parameters:
- name: PV
  required: true
- name: PATH
  value: /opt/pv
  required: true
EOF
 
 
### PV
```

는 시스템 어드민으로 만들어야 함

```
.
$ oc login -u system:admin
$ for NO in {01..04}; do oc new-app --param PV=$NO -f pv.yml; done
 
### 
```

생성한 `PV` 확인  
`$ oc get pv`  
   
   
프로젝트 및 APP 생성  
`###` 프로젝트 및 `APP` 생성은 일반 계정으로 진행  

```
$ oc login -u admin -p admin
 
$ oc new-project 3scale-amp
 
 
### github
```

의 `3scale`에 있는 `AMP` 용 `YAML` 파일을 이용해 `APP` 생성  
`### WILDCARD_DOMAIN` 의 값은 `openshift` 클러스터의 `openshift_master_default_subdomain` 값을 지정  

```
$ oc new-app \
  --file https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.1.0-GA/amp/amp.yml \
  --param WILDCARD_DOMAIN=apps.openshift.3scale
```
    
앱을 생성하면 아래와 같이 자동생성된 admin 계정 정보가 노출됨. 이후 웹콘솔에 로그인할 때 사용해야 함,  
   
설치 확인  
`### PV` 와 `PVC`가 `bind`되었는지 확인  

```
$ oc get pvc
 
### POD 
```

상태 확인  

```
$ watch -n 3 'oc get po'
```
    
어드민 웹콘솔 접속  
어드민 웹콘솔 주소 확인하여 접속 ([https://3scale-admin.apps.openshift.3scale](https://3scale-admin.apps.openshift.3scale/))  

```
$ oc get route system-provider-admin-route
NAME                          HOST/PORT                            PATH      SERVICES          PORT      TERMINATION   WILDCARD
system-provider-admin-route   3scale-admin.apps.openshift.3scale             system-provider   http      edge/Allow    None
```
 도메인을 찾을 수 없는 경우 192.168.100.40을 DNS로 등록해주어야 함.
 
==\>\> 현재의 AMP 도메인:  [https://3scale-admin.amp.skhynix.cloud/](https://3scale-admin.amp.skhynix.cloud/)  
   
3Scale AMP 제거 방법  
프로젝트를 지우는 것이 가장 편함. PV는 제거 후 재생성해야 함.  

```
$ oc delete project 3scale-amp
$ oc login -u system:admin
$ oc delete pv pv01 pv02 pv03 pv04
$ for NO in {01..04}; do oc new-app --param PV=$NO -f pv.yml; done
```
 \> 출처: \<[https://wiki.bliex.com/pages/viewpage.action?pageId=103317586](https://wiki.bliex.com/pages/viewpage.action?pageId=103317586)\>