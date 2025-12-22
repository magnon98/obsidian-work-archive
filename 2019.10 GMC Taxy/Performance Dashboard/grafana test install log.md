```
sudo yum install -y git nodejs  
sudo npm i -g npm
```
 
```
sudo yum install [https://dl.grafana.com/oss/release/grafana-6.4.3-1.x86_64.rpm](https://dl.grafana.com/oss/release/grafana-6.4.3-1.x86_64.rpm)
```
   

```
sudo systemctl start grafana-server  
sudo systemctl enable grafana-server
```
 
```
sudo firewall-cmd --add-port=3000/tcp  
sudo firewall-cmd --runtime-to-permanent
```
   

```
[http://192.168.100.36:3000/](http://192.168.100.36:3000/)  
admin // admin ==\> admin // qmfflrtm
```
   

```
sudo grafana-cli plugins install grafana-simple-json-datasource
```
   

```
sudo systemctl restart grafana-server
```
    
```
git clone [https://github.com/bergquist/fake-simple-json-datasource](https://github.com/bergquist/fake-simple-json-datasource)  
sudo mv fake-simple-json-datasource /opt/  
cd /opt/fake-simple-json-datasource  
npm i
```
 
```
sudo firewall-cmd --add-port=3333/tcp  
sudo firewall-cmd --runtime-to-permanent
```
 
```
node index.js
```