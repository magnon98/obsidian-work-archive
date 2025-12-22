```
curl -O [https://downloads.jboss.org/keycloak/11.0.0/keycloak-11.0.0.tar.gz](https://downloads.jboss.org/keycloak/11.0.0/keycloak-11.0.0.tar.gz)  
tar zxf keycloak-11.0.0.tar.gz  
sudo mv keycloak-11.0.0 /opt/
```
 
```
sudo groupadd -r wildfly  
sudo useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly
```
 
```
sudo ln -s /opt/keycloak-11.0.0 /opt/wildfly  
sudo chown -R wildfly:wildfly /opt/keycloak-11.0.0 /opt/wildfly
```
    
```
sudo mkdir /etc/wildfly  
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly/  
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system/  
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin/  
sudo chmod +x /opt/wildfly/bin/launch.sh
```
 
```
sudo systemctl enable wildfly.service  
sudo systemctl start wildfly.service  
systemctl status wildfly.service
```
         

```
Keycloak Default Login UI: [http://keycloak.bliex.io:8080/auth/realms/default/account/](http://keycloak.bliex.io:8080/auth/realms/default/account/)  
ID: bliex  
PW: qmfflrtm
```
 
```
Keycloak NIA Login UI: [http://keycloak.bliex.io:8080/auth/realms/nia/account/](http://keycloak.bliex.io:8080/auth/realms/nia/account/)  
ID: bliex  
PW: qmfflrtm
```
   

```
[https://www.keycloak.org/downloads](https://www.keycloak.org/downloads)
```