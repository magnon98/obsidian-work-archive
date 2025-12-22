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
sudo yum install -y yum-utils yum-plugin-priorities java-1.8.0-openjdk-devel wget   
EOF  
done
```
    
```
### 설치용 파일 복사할 디렉토리 생성  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo mkdir /opt/installers  
sudo chown apigee:apigee /opt/installers  
EOF  
done
```
    
```
### 여기부터는 apigee 계정으로
```
 
```
for i in {90..99}; do scp -r /opt/installers/* apigee$i:/opt/installers/; done
```
    
```
### bootstrap 다운로드  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
curl [https://software.apigee.com/bootstrap_4.19.01.sh](https://software.apigee.com/bootstrap_4.19.01.sh) -o /opt/installers/bootstrap_4.19.01.sh  
EOF  
done
```
    
```
### bootstrap 실행  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
sudo /bin/bash /opt/installers/bootstrap_4.19.01.sh apigeeuser=ebaykorea apigeepassword=_Ukwzvyi_oiSIN5A  
EOF  
done
```
    
```
### apigee repo 확인  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
cat /etc/yum.repos.d/apigee.repo  
EOF  
done
```
    
```
### setup파일 설치  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
/opt/apigee/apigee-service/bin/apigee-service apigee-setup install  
EOF  
done
```
    
```
###   
for i in {90..99}; do scp /tmp/apigee.config apigee$i; done
```
         

```
### 1 ~ 3  
cat \<\<EOF | sudo tee /etc/security/limits.d/90-apigee-limits.conf  
apigee soft memlock unlimited  
apigee hard memlock unlimited  
apigee soft nofile 32768  
apigee hard nofile 65536  
apigee soft as unlimited  
apigee hard as unlimited  
EOF
```
 
```
/opt/apigee/apigee-setup/bin/setup.sh -p ds -f /tmp/apigee.config  
/opt/apigee/apigee-service/bin/apigee-service apigee-zookeeper enable_autostart  
/opt/apigee/apigee-service/bin/apigee-service apigee-cassandra enable_autostart
```
    
```
### 4, 5  
/opt/apigee/apigee-setup/bin/setup.sh -p rmp -f /tmp/apigee.config  
### remove conf from /opt/nginx/conf.d
```
      

```
ssh apigee95 /bin/bash \<\<EOF  
/opt/apigee/apigee-setup/bin/setup.sh -p qs -f /tmp/apigee.config  
EOF
```
 
```
ssh apigee96 /bin/bash \<\<EOF  
/opt/apigee/apigee-setup/bin/setup.sh -p qs -f /tmp/apigee.config  
EOF
```
      

```
ssh apigee97 /bin/bash \<\<EOF  
/opt/apigee/apigee-setup/bin/setup.sh -p ps -f /tmp/apigee.config  
EOF
```
 
```
ssh apigee98 /bin/bash \<\<EOF  
/opt/apigee/apigee-setup/bin/setup.sh -p ps -f /tmp/apigee.config  
EOF
```
      

```
ssh apigee99 /bin/bash \<\<EOF  
/opt/apigee/apigee-setup/bin/setup.sh -p ms -f /tmp/apigee.config  
/opt/apigee/apigee-service/bin/apigee-service edge-ui restart  
EOF
```
      

```
### test installation
```
 
```
/opt/apigee/apigee-service/bin/apigee-service apigee-validate install  
/opt/apigee/apigee-service/bin/apigee-service apigee-validate setup -f /tmp/apigee.config
```
                  

```
### 제거  
for i in {90..99}; do ssh apigee$i /bin/bash \<\<EOF  
/opt/apigee/apigee-service/bin/apigee-all stop  
sudo yum clean all  
sudo rpm -e $(rpm -qa | egrep "(apigee-|edge-)")  
sudo rm -rf /opt/apigee/* /opt/apigee/.pki /opt/nginx  
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