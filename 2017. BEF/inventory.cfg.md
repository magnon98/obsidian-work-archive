# ansible-playbook -u ec2-user -b -i inventory/inventory.cfg cluster.yml --private-key=~/.ssh/ec2_virginia_k8s.pem  
master01 ansible_port=22 ansible_host=34.193.52.135  ip=172.31.41.95  
master02 ansible_port=22 ansible_host=34.200.193.196 ip=172.31.43.171  
worker01 ansible_port=22 ansible_host=34.225.51.162  ip=172.31.41.193  
[etcd]  
master01  
master02  
[kube-master]  
master01  
master02  
[kube-node]  
worker01  
[k8s-cluster:children]  
kube-node  
kube-master