### ec2-personalize 실행
 
### ssh 접속용 인증서 설정
 
###  nginx repo  추가  
$ cat \<\<EOF | sudo tee /etc/yum.repos.d/nginx.repo  
[nginx]  
name=nginx repo  
baseurl=http://nginx.org/packages/rhel/7/\$basearch/  
gpgcheck=0  
enabled=1  
EOF
 
### nginx 설치  
$ sudo yum install nginx  
$ sudo systemctl start nginx  
$ sudo systemctl status nginx  
$ sudo systemctl enable nginx
 
### apiserver.pem 복사 (bef-dev-kube-m101 --\> bef-dev-www)  
$ ssh bef.dev.m101 sudo cat /etc/kubernetes/ssl/apiserver.pem | ssh bef.dev.www sudo tee /etc/pki/tls/certs/apiserver.pem
   

### reverse proxy 설정  
upstream upstream_prometheus {  
server 50.1.111.187:30703;  
server 50.1.111.188:30703;  
server 50.1.111.189:30703;  
}  
server {  
listen 30703;  
location / {  
proxy_pass [http://upstream_prometheus](http://upstream_prometheus);  
}  
}
   

```
upstream upstream_portal_was {  
server 127.0.0.1:8080;  
}  
upstream upstream_apiserver {  
server 50.1.111.187:6443;  
server 50.1.111.188:6443;  
server 50.1.111.189:6443;  
}  
server {  
listen 80;  
location /app {  
proxy_pass [http://upstream_portal_was](http://upstream_portal_was);  
}  
location /api {  
proxy_pass [https://upstream_apiserver](https://upstream_apiserver);  
proxy_pass_header Authorization;  
proxy_ssl_name /etc/pki/tls/certs/apiserver.pem;  
}  
location =/ {  
proxy_pass [https://upstream_apiserver](https://upstream_apiserver);  
proxy_pass_header Authorization;  
proxy_ssl_name /etc/pki/tls/certs/apiserver.pem;  
}  
}
```
      

### node.js repo 추가  
$ sudo -i  
# curl --silent --location [https://rpm.nodesource.com/setup_6.x](https://rpm.nodesource.com/setup_6.x) | bash -  
### node.js 설치  
$ sudo yum install gcc-c++ make nodejs