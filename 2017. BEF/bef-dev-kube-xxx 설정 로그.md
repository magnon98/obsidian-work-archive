### ec2-personalize 실행
 
### ssh 접속용 인증서 설정
 
### firewalld 서비스 중지  
$ sudo systemctl stop firewalld  
$ sudo systemctl disable firewalld
 
### inventory file 생성  
\<개발용 kube cluster\>

|   |
|---|
|```<br>bef-dev-kube-m101 ansible_port=22 ansible_host=50.1.111.187 ip=50.1.111.187  <br>bef-dev-kube-m102 ansible_port=22 ansible_host=50.1.111.188 ip=50.1.111.188  <br>bef-dev-kube-m103 ansible_port=22 ansible_host=50.1.111.189 ip=50.1.111.189  <br>bef-dev-kube-w101 ansible_port=22 ansible_host=50.1.111.190 ip=50.1.111.190<br>```<br><br>  <br><br>```<br>[etcd]  <br>bef-dev-kube-m101  <br>bef-dev-kube-m102  <br>bef-dev-kube-m103<br>```<br><br>  <br><br>```<br>[kube-master]  <br>bef-dev-kube-m101  <br>bef-dev-kube-m102  <br>bef-dev-kube-m103<br>```<br><br>  <br><br>```<br>[kube-node]  <br>bef-dev-kube-w101<br>```<br><br>  <br><br>```<br>[k8s-cluster:children]  <br>kube-master  <br>kube-node<br>```|

\<테스트용 kube cluster\>

|   |
|---|
|```<br>bef-dev-kube-m201 ansible_port=22 ansible_host=50.1.111.191 ip=50.1.111.191  <br>bef-dev-kube-m202 ansible_port=22 ansible_host=50.1.111.192 ip=50.1.111.192  <br>bef-dev-kube-m203 ansible_port=22 ansible_host=50.1.111.193 ip=50.1.111.193  <br>bef-dev-kube-w201 ansible_port=22 ansible_host=50.1.111.194 ip=50.1.111.194<br>```<br><br>  <br><br>```<br>[etcd]  <br>bef-dev-kube-m201  <br>bef-dev-kube-m202  <br>bef-dev-kube-m203<br>```<br><br>  <br><br>```<br>[kube-master]  <br>bef-dev-kube-m201  <br>bef-dev-kube-m202  <br>bef-dev-kube-m203<br>```<br><br>  <br><br>```<br>[kube-node]  <br>bef-dev-kube-w201<br>```<br><br>  <br><br>```<br>[k8s-cluster:children]  <br>kube-master  <br>kube-node<br>```|
 
### ping-pong 테스트  
$ ansible all -m ping -k -u bef -i inventory/dev1.cfg --private-key=~/.ssh/bef_dev_rsa
 
### k8s 설치  
$ ansible-playbook -u bef -b -i inventory/dev1.cfg cluster.yml --private-key=~/.ssh/bef_dev_rsa
 
### k8s 설치 확인  
$ kubectl cluster-info  
$ kubectl get event