```
### setup.conf 파일 수정  
  - IP  
  - Password  
  - SMTP
```
    
```
### apigee user 생성
```
 
```
sudo useradd -m -s /bin/bash apigee  
echo 'qmfflrtm' | sudo passwd apigee --stdin  
sudo usermod -aG wheel apigee  
echo -e apigee"\tALL=(ALL)\tNOPASSWD: ALL" | sudo tee -a /etc/sudoers
```
    
```
###########################################################################
```
   

```
### ipv6 비활성화  
sudo sed -i 's/^\:\:1/#\:\:1/' /etc/hosts  
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1  
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1  
hostname -i
```
   

```
### disable selinux  
sudo sed -i 's/^SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config  
sudo setenforce 0
```
 
```
### disable firewalld  
sudo systemctl stop firewalld  
sudo systemctl disable firewalld
```
   

```
### install epel repo  
sudo yum install -y [https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm](https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm)
```
 
```
## CentOS 7  
sudo yum install -y epel-release
```
 
```
## RHEL 7  
sudo subscription-manager repos --enable="rhel-7-server-extras-rpms"
```
   

```
###########################################################################
```
   

```
### 필수 유틸 설치  
sudo yum install -y yum-utils yum-plugin-priorities java-1.8.0-openjdk-devel wget net-tools unzip
```
   

```
### 설치용 파일 복사
```
   

```
### bootstrap 실행  
sudo /bin/bash /opt/installers/bootstrap_4.19.01.sh apigeeuser=ebaykorea apigeepassword=_Ukwzvyi_oiSIN5A
```
 
```
### setup파일 설치  
/opt/apigee/apigee-service/bin/apigee-service apigee-setup install
```
   

```
###########################################################################
```
   

```
##################### install datastore - 1 ~ 3  
sudo cp /opt/installers/90-apigee-limits.conf /etc/security/limits.d/  
/opt/apigee/apigee-setup/bin/setup.sh -p ds -f /opt/installers/setup.config
```
 
```
apigee-all status
```
 
```
### check zookeeper  
telnet \<IP\> 2181  
ruok
```
   

```
### check cassandra  
/opt/apigee/apigee-cassandra/bin/nodetool status
```
   

```
##################### install management server - 1  
/opt/apigee/apigee-setup/bin/setup.sh -p ms -f /opt/installers/setup.config  
/opt/apigee/apigee-service/bin/apigee-service edge-ui restart
```
 
```
### check  
curl -u magnon@bliex.com -v [http://localhost:8080/v1/organizations](http://localhost:8080/v1/organizations)  
curl -u magnon@bliex.com -v [http://localhost:8080/v1/users](http://localhost:8080/v1/users)
```
       
```
###################### install rmp - 4, 5  
/opt/apigee/apigee-setup/bin/setup.sh -p rmp -f /opt/installers/setup.config  
### remove conf from /opt/nginx/conf.d  
find /opt/nginx/conf.d/ -type f -exec mv {} {}.old \;
```
 
```
### restart nginx  
apigee-service edge-router restart
```
   

```
### check  
apigee-all status
```
 
```
### check router  
curl [http://localhost:8081/v1/servers/self/status](http://localhost:8081/v1/servers/self/status)
```
 
```
### check message processor  
curl [http://localhost:8082/v1/servers/self/status](http://localhost:8082/v1/servers/self/status)
```
      

```
###################### install qpid - 6, 7  
/opt/apigee/apigee-setup/bin/setup.sh -p qs -f /opt/installers/setup.config
```
   

```
### check  
apigee-all status  
curl [http://localhost:8083/v1/servers/self/status](http://localhost:8083/v1/servers/self/status)
```
    
```
###################### install postgres 8, 9  
/opt/apigee/apigee-setup/bin/setup.sh -p ps -f /opt/installers/setup.config
```
 
```
### check  
apigee-all status
```
    
```
### check master - standby  
apigee-service apigee-postgresql postgres-check-master  
apigee-service apigee-postgresql postgres-check-standby
```
    
```
##########################################################################
```
    
```
### test installation - 1
```
 
```
/opt/apigee/apigee-service/bin/apigee-service apigee-validate install  
/opt/apigee/apigee-service/bin/apigee-service apigee-validate setup -f /opt/installers/setup.config
```
      

```
##########################################################################
```
    
```
### 노드 클린징  
/opt/apigee/apigee-service/bin/apigee-all stop  
sudo yum clean all  
sudo rpm -e $(rpm -qa | egrep "(apigee-|edge-)")  
sudo rm -rf /opt/apigee /opt/nginx
```
   

```
### 특정 서비스 삭제  
apigee-service [서비스명] uninstall
```