```
### sudoer nopasswd 설정  
echo -e $USER"\tALL=(ALL)\tNOPASSWD: ALL" | sudo tee -a /etc/sudoers
```
    
```
### apigee user 생성
```
 
```
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo useradd -m -s /bin/bash apigee  
echo 'qmfflrtm' | sudo passwd apigee --stdin  
echo -e apigee"\tALL=(ALL)\tNOPASSWD: ALL" | sudo tee -a /etc/sudoers  
EOF  
done
```
 
```
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
echo -n "apigee$i: "  
id apigee  
EOF  
done
```
    
```
### ipv6 비활성화  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo sed -i 's/^\:\:1/#\:\:1/' /etc/hosts  
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1  
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1  
EOF  
done
```
 
```
### 확인  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
echo -n "apigee$i: "  
hostname -i  
EOF  
done
```
   

```
### disable selinux  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo sed -i 's/^SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config  
sudo setenforce 0  
EOF  
done
```
 
```
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
echo -n "apigee$i: "  
sudo getenforce  
EOF  
done
```
   

```
### disable firewalld  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo systemctl stop firewalld  
sudo systemctl disable firewalld  
EOF  
done
```
 
```
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
echo -n "apigee$i: "  
sudo systemctl status firewalld | grep "Active:"  
EOF  
done
```
         

```
### install epel repo  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo yum install -y [https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm](https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm)  
EOF  
done
```
       
```
### libdb4 체크  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
echo apigee$i  
/usr/bin/rpm -qa | grep libdb4  
EOF  
done
```
    
```
### yum util, openjdk 설치  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo yum install -y yum-utils yum-plugin-priorities java-1.8.0-openjdk-devel wget net-tools unzip  
EOF  
done
```
      

```
##########################################################################
```
       
```
############ 노드별 공통 작업
```
   

```
### 설치용 파일 복사  
for i in {90..99}; do  
scp -r /opt/installers apigee$i:/tmp/  
ssh apigee$i /bin/bash \<\<EOF  
sudo cp -r /tmp/installers /opt/  
sudo chown -R apigee:apigee /opt/installers  
EOF  
done
```
   

```
### bootstrap 실행  
### curl [https://software.apigee.com/bootstrap_4.19.01.sh](https://software.apigee.com/bootstrap_4.19.01.sh) -o /tmp/bootstrap_4.19.01.sh
```
 
```
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo mkdir /opt/apigee  
sudo chown apigee:apigee /opt/apigee  
sudo /bin/bash /opt/installers/bootstrap_4.19.01.sh apigeeuser=ebaykorea apigeepassword=_Ukwzvyi_oiSIN5A  
EOF  
done
```
   

```
### setup파일 설치  
/opt/apigee/apigee-service/bin/apigee-service apigee-setup install
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
curl -u magnon@bliex.com -v [http://localhost:8080/v1/](http://localhost:8080/v1/users)users
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
curl [http://localhost:808](http://localhost:8082/v1/servers/self/status)2/v1/servers/self/status
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
### 제거  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
/opt/apigee/apigee-service/bin/apigee-all stop  
sudo yum clean all  
sudo rpm -e $(rpm -qa | egrep "(apigee-|edge-)")  
sudo rm -rf /opt/apigee /opt/nginx  
EOF  
done
```
   

```
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
echo apigee$i  
sudo userdel -r apigee  
sudo userdel -r keyadmin  
sudo groupdel apigee  
EOF  
done
```