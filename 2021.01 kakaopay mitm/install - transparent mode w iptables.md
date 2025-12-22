```
#!/bin/bash
```
 
```
set -x 
```
 
```
MITMPROXY_HOME=/opt/mitmproxy  
GSUITE_DOMAIN='bliex.com'
```
 
```
MIN=1  
MAX=5  
NIC_NAME=eth0
```
    
```
### ============================================================================  
### install mitmproxy on VM  
### ============================================================================
```
   

```
sudo useradd mitmproxy -d $MITMPROXY_HOME -s /bin/bash  
sudo mkdir -p $MITMPROXY_HOME/bin  
sudo chown -R mitmproxy:mitmproxy $MITMPROXY_HOME
```
   

```
sudo -u mitmproxy tar zxf mitmproxy-6.0.2-linux.tar.gz -C $MITMPROXY_HOME/bin  
sudo -u mitmproxy tar xf mitmproxy_certs.tar -C $MITMPROXY_HOME
```
    
```
cat \<\<EOF | sudo -u mitmproxy tee $MITMPROXY_HOME/google_apps_header.py  
def request(flow):  
    if flow.request.pretty_host.index("google.com") \> 1:  
        flow.request.headers["X-GoogApps-Allowed-Domains"] = "$GSUITE_DOMAIN"  
EOF
```
    
```
cat \<\<EOF | sudo -u mitmproxy tee $MITMPROXY_HOME/.mitmproxy/config.yaml  
scripts:  
- $MITMPROXY_HOME/google_apps_header.py  
EOF
```
    
```
### ============================================================================  
### prepare mitmproxy as systemd service  
### ============================================================================
```
 
```
### create service exec script file  
echo '#!/bin/bash
```
 
```
[[ -d $HOME/logs ]] || mkdir $MITMPROXY_HOME/logs
```
 
```
$HOME/bin/mitmdump --mode transparent -p $1 \>\> $HOME/logs/mitm_$1_$(date +"%Y%m%d").log' \  
    | sudo -u mitmproxy tee $MITMPROXY_HOME/mitmproxy-service.sh \> /dev/null
```
 
```
chmod a+x $MITMPROXY_HOME/mitmproxy-service.sh
```
         

```
### create systemd service file  
for ((i=$MIN; i \<= $MAX; i++)); do  
    ii=$([ $i -lt 10 ] && echo '0'$i || echo $i)
```
 
```
cat \<\<EOF | sudo tee /etc/systemd/system/mitmproxy$ii.service \> /dev/null  
[Unit]  
Description=mitmproxy module #$ii  
After=network-online.target  
Wants=network-online.target systemd-networkd-wait-online.service
```
 
```
[Service]  
User=mitmproxy  
ExecStart=$MITMPROXY_HOME/mitmproxy-service.sh 188$ii  
Restart=on-failure  
RestartSec=3s
```
 
```
[Install]  
WantedBy=multi-user.target  
EOF  
done
```
       
```
### create iptable rules  
MIN=1  
MAX=5  
for ((i=$MIN; i \<= $MAX; i++)); do  
    ii=$([ $i -lt 10 ] && echo '0'$i || echo $i)
```
 
```
    if [[ $i -lt $MAX ]]; then  
        sudo iptables -t nat -A PREROUTING -i $NIC_NAME -p tcp --dport 80 \  
            -j REDIRECT --to-port 188$ii -m statistic --mode nth --every $MAX --packet $(($i - 1))  
        sudo iptables -t nat -A PREROUTING -i $NIC_NAME -p tcp --dport 443 \  
            -j REDIRECT --to-port 188$ii -m statistic --mode nth --every $MAX --packet $(($i - 1))  
    else  
        sudo iptables -t nat -A PREROUTING -i $NIC_NAME -p tcp --dport 80 \  
            -j REDIRECT --to-port 188$ii -m statistic --mode nth --every 1 --packet 0  
        sudo iptables -t nat -A PREROUTING -i $NIC_NAME -p tcp --dport 443 \  
            -j REDIRECT --to-port 188$ii -m statistic --mode nth --every 1 --packet 0  
    fi  
done
```
    
```
for ((i=$MIN; i \<= $MAX; i++)); do  
    ii=$([ $i -lt 10 ] && echo '0'$i || echo $i)  
    sudo systemctl enable mitmproxy$ii.service  
    sudo systemctl start mitmproxy$ii.service  
done
```