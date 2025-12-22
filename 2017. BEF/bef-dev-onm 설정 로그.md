### ec2-personalize 실행
 
### ssh 접속용 인증서 설정
 
### openJDK 설치  
$ sudo yum install java
 
### SELinux 비활성화  
$ sudo setenforce 0  
$ sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
 
### Jeknins repo 추가  
$ sudo wget -O /etc/yum.repos.d/jenkins.repo [http://pkg.jenkins-ci.org/redhat/jenkins.repo](http://pkg.jenkins-ci.org/redhat/jenkins.repo)  
$ sudo rpm --import [https://jenkins-ci.org/redhat/jenkins-ci.org.key](https://jenkins-ci.org/redhat/jenkins-ci.org.key)
 
### Jenkins 설치  
$ sudo yum install jenkins
 
### Jenkins 실행  
$ sudo systemctl start jenkins  
$ sudo systemctl enable jenkins
 
### firewalld runtime 설정  
$ sudo firewall-cmd --add-port=8080/tcp
   

### 브라우저로 [http://50.1.111.186:8080](http://50.1.111.186:8080) 접속 확인
   

### firewalld runtime 설정을 영구 적용  
$ sudo firewall-cmd --runtime-to-permanent
   

### 초기 admin 패스워드 확인  
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword  
f6bc07085dfa452fbf273a0e9b4a4fe5
   

### 브라우저에서 로그인 후 install suggested plugin 선택
   

### 어드민 계정 생성  
admin // bef+xn2 // five@exntu.com
   

```
$ sudo yum install urw-fonts  
$ wget [https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-4.4.1-1.x86_64.rpm](https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-4.4.1-1.x86_64.rpm)  
$ rpm -Uvh grafana-4.4.1-1.x86.rpm  
$ sudo systemctl daemon-reload  
$ sudo systemctl start grafana-server  
$ sudo systemctl enable grafana-server  
$ sudo firewall-cmd --add-port=3000/tcp
```
   

### node.js repo 추가  
$ sudo -i  
# curl --silent --location [https://rpm.nodesource.com/setup_6.x](https://rpm.nodesource.com/setup_6.x) | bash -  
### node.js 설치  
$ sudo yum install gcc-c++ make nodejs  
$ which node  
$ node -v  
$ which npm  
$ npm -v  
### angular cli  설치  
$ sudo npm install -g @angular/cli  
$ which ng  
$ ng version