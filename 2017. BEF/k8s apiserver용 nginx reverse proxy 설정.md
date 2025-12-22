```
### generate private ssl certificate  
$ openssl genrsa -des3 -out nginx_ssl.key.orig 1024  
$ openssl req -new -key nginx_ssl.key.orig -out nginx_ssl.csr  
$ openssl rsa -in nginx_ssl.key.orig -out nginx_ssl.key  
$ openssl x509 -req -days 365 -in nginx_ssl.csr -signkey nginx_ssl.key -out nginx_ssl.crt  
$ sudo cp nginx_ssl.crt nginx_ssl.key /etc/pki/tls/certs/
```
 
```
### copy apiserver cert  
$ sudo cp ~/apiserver.pem /etc/pki/tls/certs/
```
 
```
### install nginx  
$ cat \<\<EOF | sudo tee /etc/yum.repos.d/nginx.repo  
[nginx]  
name=nginx repo  
baseurl=http://nginx.org/packages/rhel/7/\$basearch/  
gpgcheck=0  
enabled=1  
EOF  
$ sudo yum install nginx  
$ sudo systemctl enable nginx  
$ sudo systemctl start nginx
```
 
```
### create reverse proxy conf  
$ cat \<\<EOF | sudo tee /etc/nginx/conf.d/reverse_proxy.conf  
upstream k8s_master {  
server 10.0.100.58:6443;  
}  
server {  
listen 443;  
ssl                 on;  
ssl_certificate     /etc/pki/tls/certs/nginx_ssl.crt;  
ssl_certificate_key /etc/pki/tls/certs/nginx_ssl.key;  
location / {  
proxy_pass        [https://k8s_master](https://k8s_master);  
proxy_pass_header Authorization;  
proxy_ssl_name    /etc/pki/tls/certs/apiserver.pem;  
}  
}  
EOF  
$ sudo systemctl restart nginx
```
 
```
### test  
$ curl --insecure --header "Authorization: Bearer eyJhbGciOiJSUzI1N....." [https://localhost/](https://localhost/)
```