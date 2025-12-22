k8s installation procedure
 
# installer - install pip  
$ sudo /bin/sh -c 'curl [https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py) | python'
 
# installer - install dependency modules  
$ sudo yum install -y python-devel python-lxml openssl-devel gcc libffi-devel git
 
# installer - install ansible  
$ sudo pip install ansible
 
# installer - install kubespray-cli  
$ sudo pip install kubespray
   

# installer - get kubespray  
$ git clone [https://github.com/kubernetes-incubator/kubespray.git](https://github.com/kubernetes-incubator/kubespray.git) ~/kubespray  
$ cd ~/kubespray  
$ git reset --hard 7a72b2d5585e3b527c7571270f7e3ef1d90a97cf  
$ git clone [https://gitlab.com/bliex/k8s/kubebot.git](https://gitlab.com/bliex/k8s/kubebot.git) ~/kubebot
   

# installer - override settings  
$ cp -r ~/kubebot/* ~/kubespray
   

# installer - disable helm  
$ vi inventory/group_vars/k8s-cluster.yml  
helm_enabled: false
   

# aws - change hostname  
$ echo "preserve_hostname: true" | sudo tee --append /etc/cloud/cloud.cfg  
$ echo "master02" | sudo tee /etc/hostname  
$ sudo reboot
   

# aws - update & reboot  
$ sudo yum update -y  
$ sudo reboot
   

# installer - modify node info inside inventory/inventory.cfg  
# public ip to 'ansible_host'  
# internal ip to 'ip'
   

# installer - ping test via ansible  
$ ansible all -m ping -k -u ec2-user -i ~/inventory/inventory.cfg --private-key=~/.ssh/ec2_virginia_k8s.pem
   

# installer - setup k8s  
$ cd ~/kubespray  
$ ansible-playbook -u ec2-user -b -i inventory/inventory.cfg cluster.yml --private-key=~/.ssh/ec2_virginia_k8s.pem
   

# installer - howto add additional node  
# add info to inventory/inventory.cfg and...  
$ cd ~/kubespray  
$ ansible-playbook -u ec2-user -b -i inventory/inventory.cfg upgrade-cluster.yml --private-key=~/.ssh/ec2_virginia_k8s.pem
    
# aws - kubectl auto-completino  
$ sudo yum install bash-completion -y  
$ source \<(kubectl completion bash)