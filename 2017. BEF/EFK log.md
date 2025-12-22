```
====
```
 
```
kubectl --namespace=kube-system delete -f /etc/kubernetes/elasticsearch-deployment.yaml  
kubectl --namespace=kube-system delete -f /etc/kubernetes/elasticsearch-service.yaml  
kubectl --namespace=kube-system delete -f /etc/kubernetes/fluentd-ds.yaml  
kubectl --namespace=kube-system delete -f /etc/kubernetes/kibana-deployment.yaml  
kubectl --namespace=kube-system delete -f /etc/kubernetes/kibana-service.yaml  
sudo rm -f /etc/kubernetes/elasticsearch* /etc/kubernetes/fluentd* /etc/kubernetes/kibana*  
kubectl --namespace=kube-system get pod  
kubectl --namespace=kube-system get service
```
   

```
========================================================================================
```
   

```
### Import the Elastic PGP Key  
$ sudo rpm --import [https://artifacts.elastic.co/GPG-KEY-elasticsearch](https://artifacts.elastic.co/GPG-KEY-elasticsearch)
```
    
```
### Installing from the RPM repository  
$ cat \<\<EOF | sudo tee /etc/yum.repos.d/kibana.repo  
[elasticsearch-5.x]  
name=Elasticsearch repository for 5.x packages  
baseurl=https://artifacts.elastic.co/packages/5.x/yum  
gpgcheck=1  
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch  
enabled=1  
autorefresh=1  
type=rpm-md
```
 
```
[kibana-5.x]  
name=Kibana repository for 5.x packages  
baseurl=https://artifacts.elastic.co/packages/5.x/yum  
gpgcheck=1  
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch  
enabled=1  
autorefresh=1  
type=rpm-md  
EOF
```
 
```
$ sudo yum install kibana  
$ sudo systemctl start kibana  
$ sudo systemctl enable kibana
```
   

```
========================================================================================
```
       
```
sudo -i
```
 
```
yum remove -y docker-engine  
yum autoremove -y  
yum clean all
```
 
```
rm -rf /etc/bash_completion.d/kubectl.sh  
rm -rf /etc/docker  
rm -rf /etc/pki/ca-trust/source/anchors/kube-ca.crt  
rm -rf /etc/systemd/system/docker.service  
rm -rf /etc/systemd/system/docker.service.d  
rm -rf /etc/systemd/system/multi-user.target.wants/kubelet.service  
rm -rf /etc/yum.repos.d/docker.repo  
rm -rf /home/bef/.kube  
rm -rf /home/kube  
rm -rf /root/.kube  
rm -rf /var/cache/yum/x86_64/7/dockerrepo  
rm -rf /var/lib/docker  
rm -rf /var/lib/dockershim  
rm -rf /var/lib/yum/repos/x86_64/7/dockerrepo  
rm -rf /var/log/containers  
reboot
```
   

```
cat \<\<EOF | sudo tee /etc/yum.repos.d/docker.repo   
[dockerrepo]  
name=Docker Repository  
baseurl=https://yum.dockerproject.org/repo/main/centos/7  
enabled=1  
gpgcheck=1  
gpgkey=https://yum.dockerproject.org/gpg  
EOF
```
 
```
sudo yum install docker-engine -y  
sudo systemctl start docker  
sudo docker load -i ~/coreos_etcd_v3.2.4.tar.gz  
sudo docker load -i ~/coreos_flannel_v0.8.0.tar.gz  
sudo docker load -i ~/coreos_hyperkube_v1.7.3.tar.gz
```
    
```
========================================================================================
```
   

```
sudo docker run -p 9200:9200 -e "http.host=0.0.0.0" -e "transport.host=127.0.0.1" docker.elastic.co/elasticsearch/elasticsearch:5.5.2  
sudo docker run -p 5601:5601 -e "ELASTICSEARCH_URL=http://192.168.101.41:9200" docker.elastic.co/kibana/kibana:5.5.2  
sudo docker run -p 5601:30603 -e "ELASTICSEARCH_URL=http://192.168.101.41:30503" docker.elastic.co/kibana/kibana:5.5.2
```
    
```
========================================================================================
```