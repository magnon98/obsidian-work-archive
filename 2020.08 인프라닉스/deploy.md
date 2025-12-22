```
### nginx config
```
   

```
server {  
  listen        80;
```
 
```
  root /opt/cpm/cpm-ui;
```
 
```
  location = / {  
    return 301 /app/dashboard;  
  }
```
 
```
  location = /app {  
    return 301 /app/dashboard;  
  }
```
 
```
  location ~ ^/(app/)(?\<context_path\>dashboard|monitoring)/static(?\<static_path\>/.+) {  
    root        /opt/cpm/cpm-ui/$context_path/static;  
    try_files   /$static_path =404;  
    expires     30d;  
  }
```
 
```
  location ~ ^/app/config/? {  
    root        /opt/cpm/cpm-ui/monitoring;  
    try_files   /index.html =404;  
  }
```
 
```
  location ~ ^/app/(?\<context_path\>dashboard|monitoring)/? {  
    root        /opt/cpm/cpm-ui/$context_path;  
    try_files   /index.html =404;  
  }
```
 
```
  location ~ ^/api/? {
```
 
```
  }
```
 
```
  location ~ ^/auth/? {  
    proxy_read_timeout      30;  
    proxy_connect_timeout   30;  
    proxy_redirect          off;
```
 
```
    proxy_set_header Host $host;  
    proxy_set_header X-Real-IP $remote_addr;  
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
    proxy_set_header Upgrade $http_upgrade;  
    proxy_set_header Connection "Upgrade";
```
 
```
    proxy_pass [http://127.0.0.1:8000](http://127.0.0.1:8000);  
  }  
}
```

```
ui  
git repo  
cpm-ui-dashboard  
cpm-ui-monitoring
```
 
```
API base url 설정  
.env 파일의 REACT_APP_CPM_API_BASE_URL 변경 후 build
```
    
```
api  
git repo  
cpm-api
```
 
```
cmd  
java \  
    -Dspring.profiles.active=dev \  
    -Dcpm.api.logs-path=/opt/cpm-api/logs \  
    -jar /opt/cpm-api/libs/cpm-api.jar
```