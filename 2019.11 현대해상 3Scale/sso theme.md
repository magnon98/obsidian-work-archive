```
[https://codehumsafar.wordpress.com/2018/09/11/keycloak-custom-login-theme/](https://codehumsafar.wordpress.com/2018/09/11/keycloak-custom-login-theme/)
```
    
```
/opt/eap/standalone/configuration/standalone.xml  
/opt/eap/themes/hdmf/login/messages/login-messages_en.properties  
/opt/eap/themes/hdmf/login/resources/css/login.css  
/opt/eap/themes/hdmf/login/theme.properties
```
   

```
messages_ko.properties
```
      

```
echo '---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: pv-sso-theme  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 1Gi  
  nfs:  
    path: /nas/sso-theme  
    server: bastion.ocp.bliex.io  
  persistentVolumeReclaimPolicy: Retain  
' | oc create -f -
```
   

```
echo '---  
kind: PersistentVolumeClaim  
apiVersion: v1  
metadata:  
  name: pvc-sso-theme  
spec:  
  accessModes:  
    - ReadWriteOnce  
  resources:  
    requests:  
      storage: 1Gi  
' | oc create -f -
```
    
```
[https://sso-sso.apps.ocp.bliex.io/auth/realms/3scale/protocol/openid-connect/auth?client_id=devportal&redirect_uri=https://3scale.apim26.bliex.io/auth/keycloak_07b23263d93d/callback&response_type=code&scope=openid](https://sso-sso.apps.ocp.bliex.io/auth/realms/3scale/protocol/openid-connect/auth?client_id=devportal&redirect_uri=https://3scale.apim26.bliex.io/auth/keycloak_07b23263d93d/callback&response_type=code&scope=openid)
```
 
```
[https://sso-sso.apps.ocp.bliex.io/auth/realms/3scale/protocol/openid-connect/auth?client_id=devportal&redirect_uri=https://3scale.apim26.bliex.io/auth/keycloak_07b23263d93d/callback&response_type=code&scope=openid](https://sso-sso.apps.ocp.bliex.io/auth/realms/3scale/protocol/openid-connect/auth?client_id=devportal&redirect_uri=https://3scale.apim26.bliex.io/auth/keycloak_07b23263d93d/callback&response_type=code&scope=openid)
```