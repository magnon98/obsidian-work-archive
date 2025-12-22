```
sudo subscription-manager repos --enable=rhel-7-server-3scale-amp-2.5-rpms  
sudo yum install 3scale-amp-template  
/opt/amp/templates/amp.yml
```
   

```
### 프로젝트명은?  
### wildcard router 사용할지 확인  
### admin / master 암호 지정할지, random 으로 할지 확인  
###   
oc new-app -f /opt/amp/templates/amp.yml --param WILDCARD_DOMAIN=\<WILDCARD_DOMAIN\> --param WILDCARD_POLICY=Subdomain
```