```
oc new-project rhsso
```
   

```
chown -R 1000380000:nfsnobody /exports/rhsso
```
   

```
echo 'apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: rhsso  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 10Gi  
  nfs:  
    path: /exports/rhsso  
    server: etc.shinhan.local  
  persistentVolumeReclaimPolicy: Retain' | oc create -f -
```
   

```
oc new-app \  
    --name='rhsso' \  
    --template=sso72-x509-postgresql-persistent \  
    -p SSO_ADMIN_USERNAME='admin' \  
    -p SSO_ADMIN_PASSWORD='admin.!' \  
    -p SSO_REALM='apim28' \  
    -p SSO_SERVICE_USERNAME='demouser' \  
    -p SSO_SERVICE_PASSWORD='demouser.!'
```
       
```
curl -k -X POST '[https://rhsso.apps.shinhan.local/auth/realms/apim28/protocol/openid-connect/token](https://rhsso.apps.shinhan.local/auth/realms/apim28/protocol/openid-connect/token)' \  
    -d 'grant_type=client_credentials' \  
    -d 'client_id=a2755cea' \  
    -d 'client_secret=2698b56b59cfdcf6e85331fa6c02a6e5' | python -m json.tool
```