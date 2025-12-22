```
#!/bin/bash  
sudo adduser pinpoint  
sudo chown -R pinpoint:pinpoint /opt/tomcat/tomcat-webui
```
 
```
cat \<\<EOF | sudo tee /usr/lib/systemd/system/pinpoint-ui.service  
[Unit]  
Description=Tomcat8 - Pinpoint Web UI  
After=network.target syslog.target
```
 
```
[Service]  
Type=forking  
User=pinpoint  
Group=pinpoint
```
 
```
ExecStart=/opt/tomcat/tomcat-webui/bin/catalina.sh start  
ExecStop=/opt/tomcat/tomcat-webui/bin/catalina.sh stop
```
 
```
[Install]  
WantedBy=multi-user.target  
EOF
```
 
```
sudo systemctl daemon-reload
```
 
```
sudo systemctl enable pinpoint-ui  
sudo systemctl start pinpoint-ui
```
 
```
#################################################################################
```
 
```
#!/bin/bash  
sudo adduser pinpoint  
sudo chown -R pinpoint:pinpoint /opt/tomcat/tomcat-collector
```
 
```
cat \<\<EOF | sudo tee /usr/lib/systemd/system/pinpoint-collector.service  
[Unit]  
Description=Tomcat8 - Pinpoint Collector  
After=network.target syslog.target
```
 
```
[Service]  
Type=forking  
User=pinpoint  
Group=pinpoint
```
 
```
ExecStart=/opt/tomcat/tomcat-collector/bin/catalina.sh start  
ExecStop=/opt/tomcat/tomcat-collector/bin/catalina.sh stop
```
 
```
[Install]  
WantedBy=multi-user.target  
EOF
```
 
```
sudo systemctl daemon-reload
```
 
```
sudo systemctl enable pinpoint-collector  
sudo systemctl start pinpoint-collector
```
 
```
#################################################################################
```
 
```
#!/bin/bash  
sudo adduser pinpoint  
sudo chown -R pinpoint:pinpoint /opt/hbase-1.2.6  
cat \<\<EOF | sudo tee /usr/lib/systemd/system/hbase.service  
[Unit]  
Description=HBase  
After=network.target syslog.target
```
 
```
[Service]  
Type=forking  
User=pinpoint  
Group=pinpoint
```
 
```
ExecStart=/opt/hbase-1.2.6/bin/start-hbase.sh  
ExecStop=/opt/hbase-1.2.6/bin/stop-hbase.sh
```
 
```
[Install]  
WantedBy=multi-user.target  
EOF
```
 
```
sudo systemctl daemon-reload
```
 
```
sudo systemctl enable hbase  
sudo systemctl start hbase
```