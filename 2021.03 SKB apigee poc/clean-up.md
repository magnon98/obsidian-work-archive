```
### 1번 VM 에서 .bashrc 수정!!!
```
 
```
/opt/apigee/apigee-service/bin/apigee-all stop
```
 
```
yum clean all  
rpm -e $(rpm -qa | egrep "(apigee-|edge-)")  
rm -rf /opt/apigee /opt/installers /opt/nginx
```
 
```
yum remove -y net-tools bind-utils telnet java-1.8.0-openjdk-devel epel-release wget yum-utils yum-plugin-priorities  
yum autoremove -y  
yum clean all
```
      

```
### gw1 / gw2 에서도 실행
```
 
```
rm -f ~/.ssh/authorized_keys
```
 
```
rm -f ~/.bash_history  
history -c
```