sudo systemctl disable firewalld  
sudo systemctl stop firewalld
   

# sudo find / -regextype posix-extended -regex "^.*(kube|docker|flannel|calico).*$" 2\>/dev/null
 
sudo yum remove docker-engine -y  
sudo yum autoremove -y  
sudo yum clean all
 
sudo rm -rf $HOME/.kube  
sudo rm -rf /etc/bash_completion.d/kubectl.sh  
sudo rm -rf /etc/docker  
sudo rm -rf /etc/systemd/system/docker.service  
sudo rm -rf /etc/systemd/system/docker.service.d  
sudo rm -rf /etc/systemd/system/multi-user.target.wants/kubelet.service  
sudo rm -rf /etc/yum.repos.d/docker.repo  
sudo rm -rf /home/kube  
sudo rm -rf /root/.kube  
sudo rm -rf /usr/lib/firewalld/services/docker-registry.xml  
sudo rm -rf /var/lib/cni/flannel  
sudo rm -rf /var/lib/yum/repos/x86_64/7/dockerrepo  
sudo rm -rf /var/log/containers
 
# sudo rm -rf /var/lib/docker  
# sudo rm -rf /var/lib/dockershim
 
sudo reboot