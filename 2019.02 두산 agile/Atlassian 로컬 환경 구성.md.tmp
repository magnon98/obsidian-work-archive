```
Atlassian  
#################################################################  
### 프로젝트 생성  
#################################################################
```
 
```
$ oc new-project atlassian
```
   

```
#################################################################  
### AdoptOpenJDK ImageStream 생성  
#################################################################
```
 
```
$ echo 'apiVersion: image.openshift.io/v1  
kind: ImageStream  
metadata:  
  annotations:  
    openshift.io/display-name: adoptopenjdk8  
  name: adoptopenjdk8  
  namespace: atlassian  
spec:  
  tags:  
  - annotations:  
      openshift.io/display-name: adoptopenjdk8  
      supports: openjdk  
      tags: builder,adoptopenjdk  
      version: "8"  
    from:  
      kind: DockerImage  
      name: docker.io/adoptopenjdk/openjdk8:slim  
    name: slim' | oc create -f -
```
         

```
#################################################################  
### PV 생성  
#################################################################
```
 
```
$ echo '  
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: atlassian-mysql  
  labels:  
    atlassian: mysql  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 50Gi  
  claimRef:  
    namespace: atlassian  
    name: pvc-atlassian-mysql  
  nfs:  
    path: /nas/atlassian_mysql  
    server: bastion.ocp.bliex.io  
  persistentVolumeReclaimPolicy: Recycle  
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: atlassian-crowd  
  labels:  
    atlassian: crowd  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 50Gi  
  claimRef:  
    namespace: atlassian  
    name: pvc-atlassian-mysql  
  nfs:  
    path: /nas/atlassian_crowd  
    server: bastion.ocp.bliex.io  
  persistentVolumeReclaimPolicy: Recycle  
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: atlassian-jira  
  labels:  
    atlassian: jira  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 50Gi  
  claimRef:  
    namespace: atlassian  
    name: pvc-atlassian-jira  
  nfs:  
    path: /nas/atlassian_jira  
    server: bastion.ocp.bliex.io  
  persistentVolumeReclaimPolicy: Recycle  
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: atlassian-confl  
  labels:  
    atlassian: confl  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 50Gi  
  claimRef:  
    namespace: atlassian  
    name: pvc-atlassian-confl  
  nfs:  
    path: /nas/atlassian_confl  
    server: bastion.ocp.bliex.io  
  persistentVolumeReclaimPolicy: Recycle  
' | oc create -f -
```
         

```
#################################################################  
### Git credential용 secret 생성  
#################################################################
```
 
```
$ oc create secret generic git-secret \  
    --from-literal=username=root \  
    --from-literal=password='ddp!1234'
```
         

```
#################################################################  
### MySQL 설치  
#################################################################
```
 
```
######## $ oc new-app mysql -p MYSQL_USER=bliex -p MYSQL_PASSWORD=qmfflrtm -p MYSQL_DATABASE=bliex
```
 
```
$ oc set volumes dc/mysql --remove --name=mysql-data
```
 
```
$ oc set volumes dc/mysql \  
    --add \  
    --claim-name=pvc-atlassian-mysql \  
    --claim-mode='ReadWriteOnce' \  
    --claim-size='50Gi' \  
    --mount-path=/var/lib/mysql/data \  
    --name=mysql-data
```
 
```
$ oc set env dc/mysql MYSQL_MAX_CONNECTIONS=1000 MYSQL_INNODB_LOG_FILE_SIZE=268435456 
```
 
```
oc exec -it mysql-10-5q856 -- /opt/rh/rh-mysql57/root/usr/bin/mysql -u root  
create database jira character set utf8 collate utf8_bin;  
create user 'jira'@'%' identified by 'qmfflrtm';  
grant all privileges on jira.* to 'jira'@'%';
```
 
```
create database confluence character set utf8 collate utf8_bin;  
create user 'confluence'@'%' identified by 'qmfflrtm';  
grant all privileges on confluence.* to 'confluence'@'%';
```
 
```
create database crowd character set utf8 collate utf8_bin;  
create user 'crowd'@'%' identified by 'qmfflrtm';  
grant all privileges on crowd.* to 'crowd'@'%';
```
            

```
#################################################################  
### Confluence 설치  
#################################################################
```
 
```
$ oc new-app adoptopenjdk8:slim~https://git.d-platform.doosan.com/atlassian/confluence.git \  
  --name=confluence \  
  --strategy=docker \  
  --source-secret=git-secret \  
  --build-env GIT_SSL_NO_VERIFY=true \  
  -e JVM_MAXIMUM_MEMORY=4G
```
       
```
$ oc set volumes dc/confluence \  
    --add \  
    --claim-mode='ReadWriteOnce' \  
    --claim-name='pvc-atlassian-confl' \  
    --claim-size='50Gi' \  
    --mount-path='/var/atlassian/confluence'
```
    
```
$ oc expose dc/confluence
```
    
```
$ oc expose svc/confluence
```
      

```
### confluence trial key  
AAABKg0ODAoPeNptkF9LwzAUxd/zKQK+6ENGkxXHBgG3tkila52biuJLFu9moE1Lko7t25uuDuefh  
0DIued3z8nFM7zjQjrMhpiOJ8F4Qkc4ileYBXSMYrDSqMapWvOo1puyBS0BXy7B7MBcvU1wshNlK  
7oBFBk4XmLhgHd2QgPCQuSNTkiXiwp4Jba61jfrUsF+IOsKSU8deFXtgDvTQv+wdMI4MHwjSgsnQ  
DIXqvxL+E5wBsiUBG1hdWjguDcq5vPkIUqnGSp76QmM7TwMeax2oIVvluwbZQ5nBShhQ1SYrdDK9  
jsGqC+fxnxG76Ykp9mMXKe3CXmJF69omeTcH5LRMAwpYyP0FcXPZ2n8UzpGzdtqDabYPFqfiBN6M  
vyf5b418kNY+P3Jn1DAlAwwLQIVAIStKElQDXwYa+Bci8MDM6yXoFH4AhQwzWpFeC1PBHrBpAgAm  
bHRN5u0bw==X02f3
```
   

```
### connection string  
jdbc:mysql://mysql/confluence?sessionVariables=tx_isolation='READ-COMMITTED'
```
    
```
admin // qmfflrtm // magnon+confl@bliex.com
```
                     

```
#################################################################  
### Jira 설치  
#################################################################
```
 
```
$ oc new-app adoptopenjdk8:slim~https://git.d-platform.doosan.com/atlassian/jira.git \  
  --name=jira \  
  --strategy=docker \  
  --source-secret=git-secret \  
  --build-env GIT_SSL_NO_VERIFY=true \  
  -e JVM_MAXIMUM_MEMORY=4G
```
       
```
$ oc set volumes dc/jira \  
    --add \  
    --claim-mode='ReadWriteOnce' \  
    --claim-name='pvc-atlassian-jira' \  
    --claim-size='50Gi' \  
    --mount-path='/var/atlassian/jira'
```
    
```
$ oc expose dc/jira --port=8080
```
    
```
$ oc expose svc/jira
```
    
```
### jira trial key  
AAABdA0ODAoPeNp9kUtvgkAUhff8CpJu2sUQXo3VhKQWJqkNqBWrXXQz4lWnwYHcGaz++yJgqvWx4zJzz3fOmbspzPVBonTb0c1Wx37smC3dD8a6bVptbYkAYpXlOaAR8gSEBDrnimfCo/0xHQ1HvZhq/WI9AxwsPiSg9Iil+ZlQLFF9tgZvzZYiE8+zlMPWSLK19s2RGWcrwwKTFZMQMAXenk0sk9iO1lDHuxwqOX8QRXTk97rh4Yhuc467oz2L2PbBAo0YT889xIAbwF7gvUSvIYm7bkDak3BK3j8DpzaYYzYvEmXsByKzhfphCEapyDfgKSygvna9lAvVXQpR+hMKBBPJlSA33JyV2HDKXGEviGmfhJbrOk+Oa2rl5J3+uSEcK4YK0FuwVII2wCUTXLIqoaH5CNXn/5dKa/ik9LK/aJ80AGVIzJHLprwAZII8ryTfSrYeN2z9vn6bh6+OTjcsLSpWbfZa+5d6PYYf7/1p1vMv7qAGYDAsAhRBpZeVlqWkwNgQm6qXHs4nKl0r8QIUAg3m9aSgSLka6ecI1tLaPtqqcRc=X02i6
```
    
```
admin // qmfflrtm // magnon+jira@bliex.com
```
   

```
#################################################################  
### Crowd 설치  
#################################################################
```
 
```
$ oc new-app adoptopenjdk8:slim~https://git.d-platform.doosan.com/atlassian/crowd.git \  
  --name=crowd \  
  --strategy=docker \  
  --source-secret=git-secret \  
  --build-env GIT_SSL_NO_VERIFY=true \  
  -e JVM_MAXIMUM_MEMORY=4G
```
       
```
$ oc set volumes dc/crowd \  
    --add \  
    --claim-mode='ReadWriteOnce' \  
    --claim-name='pvc-atlassian-crowd' \  
    --claim-size='50Gi' \  
    --mount-path='/var/atlassian/crowd'
```
    
```
$ oc expose dc/crowd --port=8095
```
    
```
$ oc expose svc/crowd
```
      

```
### crowd trial key  
AAABKw0ODAoPeNptkM1uwjAQhO9+Cku9tAdHxCkUkCyV2lGhClA1tAipF+Mu1FLiINuh8PYkJFV/D  
3vZ2fl2di/S0uBRucW0i2k4DHvDqI+5WGDaCQdIgFNW77wuDOO2+HjDlynYPdir1yGO9zIrZa0hV  
WuBVF7vgXlbAuIWzpKQHljNIp0+oT3EC+OruZnMgeVyawpzu840HAJV5C0m9dJ6sGwjMwdtL9EKj  
IPFcQdnK59Pp/ETn4yST2I8lTr7i/wK2eTKGtALWFf3KKpsxoORRkF82Gl7/JZ4QGgXze1WGu0aR  
hAEqPnARLA7MV6ScDl4IDcrzslY3K9QGs9YVSQJr0MaRVG3PWBW5muw882zqzYzEqL2ogqTTMRPR  
yv9H+extOpdOvj92BMZhZSEMC0CFDk7Lo+DOfdrGMM4wa8nhpf67g7RAhUAgQsUUpVapP/maD4Yy  
AbBI2Wtblo=X02f3
```
   

```
jdbc:mysql://mysql/crowd?autoReconnect=true&characterEncoding=utf8&sessionVariables=tx_isolation='READ-COMMITTED'
```
   

```
admin // qmfflrtm123$ // magnon+crowd@bliex.com
```
       
```
AD 설정 
```

- ```
    Delegated Authentication
    ```
    
    ```
    Microsoft Active Directory
    ```
    
    ```
    192.168.100.60
    ```
    
    ```
    389
    ```
    
    ```
    Base DN: DC=ad,DC=bliex,DC=io
    ```
    
    ```
    Username: cn=Administrator,cn=Users,DC=ad,DC=bliex,DC=io
    ```
    
                         
```
===============================================================================================
```
 
```
oc exec confluence-28-flgrd -- cat /opt/atlassian/confluence/conf/server.xml \> confl-server.xml
```
 
```
oc create configmap confl-server-xml --from-file=./server.xml
```
 
```
oc set volumes dc/confluence \  
    --add \  
    --name=server-xml \  
    --configmap-name=confl-server-xml \  
    --mount-path=/opt/atlassian/confluence/conf/server.xml \  
    --sub-path=server.xml
```
             
```
SKPT-32 has been created, but there is a problem in adding it to the page.  
You can manually add it later using Jira macro.
```
             
```
SP1-1  
DB Connection 이 끊겨서 발생되는 것으로 보이나 DB의 설정을 확인해보면  
wait_timeout 이 8시간(28800초)으로 충분히 길게 설정되어 있고,  
저희쪽에  테스트용으로 구성한 DB와 동일한 값인데 저희쪽에서는 발생되지 않고 있어  
Azure 쪽에서도 원인 분석이 필요해 보입니다.
```
 
```
SP1-7  
confluence.apps.d-platform.doosan.com 도메인으로 접속시 증상이 발생되는 것이 확인됩니다.  
Jira / Confluence는 서비스 당 한 개의 도메인만을 설정할 수 있는데   
현재는 apps 가 빠진 [https://jira.d-platform.doosan.com](https://jira.d-platform.doosan.com) 및 [https://confluence.d-platform.doosan.com](https://confluence.d-platform.doosan.com) 가   
기본 도메인(Base URL)으로 설정되어 있어 그렇습니다.  
두산 내부에서도 상기 도메인으로 접속이 가능할 것이기 때문에 상기의 도메인 사용을 권장드립니다.
```
 
```
SP1-16  
git 연동 테스트를 위해 생성한 것으로 실제의 이슈는 아닌 것으로 보입니다.
```
 
```
SP1-18  
본문의 내용에 해당하는 jar 파일을 찾을 수 없어 본문 내용대로는 적용할 수 없습니다.
```
 
```
SP1-19  
Confluence 에서 아직 수정되지 않은 버그입니다. ([https://jira.atlassian.com/browse/CONFCLOUD-41167](https://jira.atlassian.com/browse/CONFCLOUD-41167))  
해당 에러 메시지가 출력되더라도 JIRA 이슈는 정상적으로 생성되기 때문에  
confluence의 페이지를 수동으로 편집하여 JIRA 링크를 추가할 수 있습니다.
```
 
```
SP1-20  
다양한 용량의 파일로 테스트를 진행하였으나 에러가 발생하지 않고 있습니다.
```
 
```
SP1-21  
Base URL에 https 로 시작하는 URL을 기입하는 경우 confluence 에서 제대로 인지하지 못해 발생되는 이슈로  
OCP의 configmap 을 이용하여 server.xml 파일을 업데이트하는 것으로 해결은 가능합니다.  
재배포가 필요하기 때문에 종료 및 기동하는 약 10 ~ 15분 가량 confluence를 서비스 할 수 없습니다.
```
 
```
SP1-22  
기본 도메인(Base URL)으로 설정된 [https://confluence.d-platform.doosan.com](https://confluence.d-platform.doosan.com) 으로 접속하면  
정상적으로 연결된 것을 확인할 수 있습니다. 
```