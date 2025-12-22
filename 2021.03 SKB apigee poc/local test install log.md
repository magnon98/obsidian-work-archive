```
for i in {01..05}; do   
  ovftool --name=apigee$i \  
    --datastore=datastore-ssd \  
    --diskMode=thin \  
    --network="VM Network" \  
    --disableVerification \  
    --noSSLVerify \  
    /mnt/d/vsphere/centos7_template/centos7_template.ovf \  
    vi://root:'qmfflrtm123$'@192.168.100.241  
done
```
      

```
for i in {01..05}; do   
    echo $i  
    ssh-copy-id -i ~/.ssh/ssh-keys/apigee_rsa apigee$i  
done
```
   

```
for i in {01..05}; do   
    echo $i  
    ssh apigee$i sudo rm /etc/machine-id  
    ssh apigee$i sudo systemd-machine-id-setup  
    ssh apigee$i sudo hostnamectl  
done
```
      

```
sudo yum update -y  
sudo yum install -y java-1.8.0-openjdk-devel wget net-tools yum-utils yum-plugin-priorities jq telnet
```
       
```
sudo setenforce 0  
sudo sed -i 's/^SELINUX=enforcing/SELINUX=permissive/' /etc/selinux/config
```
 
```
sudo systemctl stop firewalld  
sudo systemctl disable firewalld
```
    
```
############## sudo sysctl net.ipv6.conf.all.disable_ipv6=1  
############## echo 'net.ipv6.conf.all.disable_ipv6 = 1' | sudo tee -a /etc/sysctl.conf  
echo $(hostname -I) $HOSTNAME | sudo tee -a /etc/hosts  
hostname -i
```
    
```
sudo groupadd -r apigee  
sudo useradd -r -g apigee -d /opt/apigee -s /sbin/nologin -c "Apigee platform user" apigee
```
      

```
sudo mkdir /opt/apigee /opt/installers  
sudo chown apigee: /opt/apigee  
sudo chown bliex: /opt/installers  
curl [https://software.apigee.com/bootstrap_4.50.00.sh](https://software.apigee.com/bootstrap_4.50.00.sh) -o /opt/installers/bootstrap_4.50.00.sh
```
    
```
echo 'LlwH5f3L3C0b3L6+Q4B8wFjCsCP9hA5P1izPRBsR06YFAy2kk2BAJxIGcyGybmeN92Zdoc22BT8M  
yv4sr0eXh1qvLKzmDnwVXY2WoNLrlAsD/pkJ70/lzfXxMJMRFGMucm3YDEuxkNU6QKnhHI+naD7N  
oVqlZIgN+BtC8kA1vBMv57+C9DhXaCNptxHNjz3MWu1MI0T7qHr2e1LaGpYtUnu8pKoOWS6Yzbu+  
ya6J3NAXHfoLnh+PTMvHV47xJl9k2FSr/mM0V8f9yk0osa5ZNW8qphbXyRUAAp2YW/qd2ywjttUn  
etInOwrZu+zFq5SuGV57WKAEHYk7jvnDJzqT7Q==' \> /opt/installers/license.txt
```
    
```
for i in {01..05}; do scp ./bootstrap_4.50.00.sh ./setup.config apigee$i:/opt/installers/; done
```
       
```
### bootstrap 실행  
for i in {01..05}; do   
    ssh apigee$i sudo /bin/bash /opt/installers/bootstrap_4.50.00.sh apigeeuser=bespineval apigeepassword=N_Q5_7y95_0QKX1  
done
```
 
```
ssh apigee01 sudo /bin/bash /opt/installers/bootstrap_4.50.00.sh apigeeuser=bespineval apigeepassword=N_Q5_7y95_0QKX1  
ssh apigee02 sudo /bin/bash /opt/installers/bootstrap_4.50.00.sh apigeeuser=bespineval apigeepassword=N_Q5_7y95_0QKX1  
ssh apigee03 sudo /bin/bash /opt/installers/bootstrap_4.50.00.sh apigeeuser=bespineval apigeepassword=N_Q5_7y95_0QKX1  
ssh apigee04 sudo /bin/bash /opt/installers/bootstrap_4.50.00.sh apigeeuser=bespineval apigeepassword=N_Q5_7y95_0QKX1  
ssh apigee05 sudo /bin/bash /opt/installers/bootstrap_4.50.00.sh apigeeuser=bespineval apigeepassword=N_Q5_7y95_0QKX1
```
    
```
### apigee-setup 설치  
for i in {01..05}; do   
    ssh apigee$i /opt/apigee/apigee-service/bin/apigee-service apigee-setup install  
done
```
 
```
ssh apigee01 /opt/apigee/apigee-service/bin/apigee-service apigee-setup install  
ssh apigee02 /opt/apigee/apigee-service/bin/apigee-service apigee-setup install  
ssh apigee03 /opt/apigee/apigee-service/bin/apigee-service apigee-setup install  
ssh apigee04 /opt/apigee/apigee-service/bin/apigee-service apigee-setup install  
ssh apigee05 /opt/apigee/apigee-service/bin/apigee-service apigee-setup install
```
      

```
for i in {01..05}; do   
    ssh apigee$i sudo /bin/bash /opt/installers/bootstrap_4.50.00.sh apigeeuser=bespineval apigeepassword=N_Q5_7y95_0QKX1  
    ssh apigee$i /opt/apigee/apigee-service/bin/apigee-service apigee-setup install  
done
```
       
```
### ds 설치  
ssh apigee01 /opt/apigee/apigee-setup/bin/setup.sh -p ds -f /opt/installers/setup.config  
ssh apigee01 /opt/apigee/apigee-service/bin/apigee-all status  
ssh apigee01 /opt/apigee/apigee-cassandra/bin/nodetool status
```
 
```
ssh apigee02 /opt/apigee/apigee-setup/bin/setup.sh -p ds -f /opt/installers/setup.config  
ssh apigee02 /opt/apigee/apigee-service/bin/apigee-all status  
ssh apigee02 /opt/apigee/apigee-cassandra/bin/nodetool status
```
 
```
ssh apigee03 /opt/apigee/apigee-setup/bin/setup.sh -p ds -f /opt/installers/setup.config  
ssh apigee03 /opt/apigee/apigee-service/bin/apigee-all status  
ssh apigee03 /opt/apigee/apigee-cassandra/bin/nodetool status
```
    
```
### ms 설치  
ssh apigee01 /opt/apigee/apigee-setup/bin/setup.sh -p ms -f /opt/installers/setup.config  
ssh apigee01 /opt/apigee/apigee-service/bin/apigee-all status  
curl -u 'canape@bliex.com':'Qmfflrtm123$' -v [http://192.168.100.38:8080/v1/organizations](http://192.168.100.38:8080/v1/organizations)
```
   

```
### rmp 설치  
ssh apigee02 /opt/apigee/apigee-setup/bin/setup.sh -p rmp -f /opt/installers/setup.config  
ssh apigee02 /opt/apigee/apigee-service/bin/apigee-all status  
curl [http://192.168.100.39:8081/v1/servers/self/status](http://192.168.100.39:8081/v1/servers/self/status)  
curl [http://192.168.100.39:8082/v1/servers/self/status](http://192.168.100.39:8082/v1/servers/self/status)
```
 
```
ssh apigee03 /opt/apigee/apigee-setup/bin/setup.sh -p rmp -f /opt/installers/setup.config  
ssh apigee03 /opt/apigee/apigee-service/bin/apigee-all status  
curl [http://192.168.100.40:8081/v1/servers/self/status](http://192.168.100.40:8081/v1/servers/self/status)  
curl [http://192.168.100.40:8082/v1/servers/self/status](http://192.168.100.40:8082/v1/servers/self/status)
```
    
```
### sax 설치  
ssh apigee04 /opt/apigee/apigee-setup/bin/setup.sh -p sax -f /opt/installers/setup.config  
ssh apigee04 /opt/apigee/apigee-service/bin/apigee-all status  
curl [http://192.168.100.40:8083/v1/servers/self/status](http://192.168.100.40:8083/v1/servers/self/status)
```
    
```
### validate install  
ssh apigee01 /opt/apigee/apigee-service/bin/apigee-service apigee-validate install  
ssh apigee01 /opt/apigee/apigee-service/bin/apigee-service apigee-validate setup -f /opt/installers/setup.config
```
         

```
export ADMIN_EMAIL=canape@bliex.com  
export ADMIN_PASSWORD='Qmfflrtm123$'  
export EDGE_SERVER=192.168.100.38
```
 
```
apigee-adminapi.sh orgs envs virtual_hosts delete -o validate -e test -v default  
apigee-adminapi.sh orgs envs virtual_hosts add -o validate -e test -v default -p 59001 -a validate.bliex.io
```
            

```
##### /opt/apigee/apigee-service/bin/apigee-all stop; sudo yum clean all; sudo rpm -e $(rpm -qa | egrep "(apigee-|edge-)"); sudo rm -rf /opt/apigee /opt/nginx
```
 
```
 
```