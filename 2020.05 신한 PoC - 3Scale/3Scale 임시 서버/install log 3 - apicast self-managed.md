```
oc adm ca create-server-cert \  
    --signer-cert=/etc/origin/master/ca.crt \  
    --signer-key=/etc/origin/master/ca.key \  
    --signer-serial=/etc/origin/master/ca.serial.txt \  
    --hostnames="*.amp.shinhan.local" \  
    --cert=amp.shinhan.local.crt \  
    --key=amp.shinhan.local.key  
    
```
   

```
oc adm ca create-server-cert \  
    --signer-cert=/etc/origin/master/ca.crt \  
    --signer-key=/etc/origin/master/ca.key \  
    --signer-serial=/etc/origin/master/ca.serial.txt \  
    --hostnames="api-client" \  
    --cert=client.crt \  
    --key=client.key
```
    
```
cp ca.crt /etc/pki/ca-trust/source/anchors/openshift-ca.crt  
update-ca-trust
```
       
```
oc new-project apim28-apicast
```
 
```
oc create secret generic apicast-configuration-url-secret \  
    --from-literal=password=https://yy2bxdyb7k3eri8i@3scale-admin.amp.shinhan.local \  
    --type=kubernetes.io/basic-auth
```
 
```
oc new-app -f [https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/master/apicast-gateway/apicast.yml](https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/master/apicast-gateway/apicast.yml) \  
    --param APICAST_NAME=apicast-mutual-tls-staging \  
    --param CONFIGURATION_LOADER=lazy \  
    --param DEPLOYMENT_ENVIRONMENT=staging \  
    --param CONFIGURATION_CACHE=0
```
 
```
oc create secret tls tls-certs --cert=amp.shinhan.local.crt --key=amp.shinhan.local.key
```
 
```
oc set volume dc/apicast-mutual-tls-staging \  
    --add \  
    --name=certificates \  
    --mount-path=/var/run/secrets/apicast \  
    --secret-name=tls-certs
```
 
```
oc set env dc/apicast-mutual-tls-staging \  
    APICAST_HTTPS_PORT=8443 \  
    APICAST_HTTPS_CERTIFICATE=/var/run/secrets/apicast/tls.crt \  
    APICAST_HTTPS_CERTIFICATE_KEY=/var/run/secrets/apicast/tls.key
```
    
```
oc patch service apicast-mutual-tls-staging -p '{"spec":{"ports":[{"name":"https","port":8443,"protocol":"TCP"}]}}'
```
   

```
oc create route passthrough --service=apicast-mutual-tls-staging --port=https --hostname=mutual-tls-example-3scale-apicast-staging.amp.shinhan.local
```