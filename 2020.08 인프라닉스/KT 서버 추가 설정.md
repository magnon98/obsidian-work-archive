```
### cpm-api 실행을 위한 사용자 추가  
sudo useradd cpm-api -d /opt/cpm/cpm-api -s /sbin/nologin
```
    
```
### cpm-api 실행 스크립트용 디렉토리 생성  
sudo mkdir /opt/cpm/cpm-api/bin
```
    
```
### cpm-api 실행 스크립트 생성  
echo '#!/bin/bash
```
 
```
if [ "x$JAVA_HOME" = "x" ]; then  
    JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"  
fi
```
 
```
if [ "x$CPM_API_APP_HOME" = "x" ]; then  
    CPM_API_APP_HOME="/opt/cpm/cpm-api"  
fi
```
 
```
if [ "x$CPM_API_LOG_PATH" = "x" ]; then  
    CPM_API_LOG_PATH="$CPM_API_APP_HOME/logs"  
fi
```
 
```
$JAVA_HOME/bin/java \  
    -Dspring.profiles.active="prod" \  
    -Dcpm.api.logs-path="$CPM_API_LOG_PATH" \  
    -Xms128m -Xmx1024m \  
    -jar $CPM_API_APP_HOME/libs/cpm-api.jar' | sudo tee /opt/cpm/cpm-api/bin/launch.sh
```
    
```
### 스크립트에 실행권한 부여  
sudo chmod u+x /opt/cpm/cpm-api/bin/launch.sh
```
    
```
### 파일 및 디렉토리 권한 재설정  
sudo chown -R cpm-api:cpm-api /opt/cpm/cpm-api
```
    
```
### cpm-api service 생성  
echo '[Unit]  
Description=The CPM API Application Server  
After=syslog.target network.target  
Before=httpd.service
```
 
```
[Service]  
User=cpm-api  
ExecStart=/opt/cpm/cpm-api/bin/launch.sh  
SuccessExitStatus=143
```
 
```
[Install]  
WantedBy=multi-user.target' | sudo tee /etc/systemd/system/cpm-api.service
```
    
```
### cpm-api 서비스 자동실행 설정  
sudo systemctl enable cpm-api
```
    
```
### cpm-api 서비스 시작  
sudo systemctl start cpm-api
```
          
```
KT VM keycloak 에 cpm realm, cpm-ui-prod 클라이언트 생성
```