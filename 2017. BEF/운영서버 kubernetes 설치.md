외부에서 접속이 불가능하여 BPV-BEF-WEBU01 을 installer로 사용
   

installer에서 작업(1)  
python 버전 확인 (2.7.x)  
$ which python && python --version
    
ssh key 생성  
$ ssh-keygen -f ~/.ssh/bef_kube_rsa
   

ssh config 생성  
$ cat \<\<EOF \> ~/.ssh/config  
Host bpv.bef.kbm01  
Hostname 222.39.117.60  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpv.bef.kbm02  
Hostname 222.39.117.61  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpv.bef.kbm03  
Hostname 222.39.117.62  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpp.bef.node01  
Hostname 222.39.117.16  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpp.bef.node02  
Hostname 222.39.117.17  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpp.bef.node03  
Hostname 222.39.117.18  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpp.bef.node04  
Hostname 222.39.117.19  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpp.bef.node05  
Hostname 222.39.117.20  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpp.bef.node06  
Hostname 222.39.117.21  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa
 
Host bpp.bef.node07  
Hostname 222.39.117.22  
User suser  
IdentityFile ~/.ssh/bef_kube_rsa  
EOF
    
kube 클러스터의 각 노드에서 작업  
python 버전 확인 (2.7.x)  
$ which python && python --version
 
OS 업데이트  
$ sudo yum update -y  
$ sudo yum autoremove -y
 
suser 계정을 sudoers에 nopasswd 등록  
suser ALL=(ALL) NOPASSWD:ALL
 
firewalld 비활성화  
$ sudo systemctl disable firewalld  
$ sudo systemctl stop firewalld
 
public key를 authorized_keys로 추가
       
installer에서 작업(2)
 
pip 설치  
$ sudo /bin/sh -c 'curl [https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py) | python'
 
ansible 설치  
$ sudo pip install ansible
 
kubespray 소스 설치  
$ tar zxf kubespray.tar.gz
 
kubespray inventory 생성 ( 반드시 노드명을 hostname과 일치시켜야 함 )  
$ cd ~/kubespray  
$ cat \<\<EOF \> ./inventory/op.cfg  
BPV-BEF-KBM01 ansible_host=bpv.bef.kbm01  
BPV-BEF-KBM02 ansible_host=bpv.bef.kbm02  
BPV-BEF-KBM03 ansible_host=bpv.bef.kbm03  
BPP-BEF-NODE01 ansible_host=bpp.bef.node01  
BPP-BEF-NODE02 ansible_host=bpp.bef.node02  
BPP-BEF-NODE03 ansible_host=bpp.bef.node03  
BPP-BEF-NODE04 ansible_host=bpp.bef.node04  
BPP-BEF-NODE05 ansible_host=bpp.bef.node05  
BPP-BEF-NODE06 ansible_host=bpp.bef.node06  
BPP-BEF-NODE07 ansible_host=bpp.bef.node07
 
[etcd]  
BPV-BEF-KBM01  
BPV-BEF-KBM02  
BPV-BEF-KBM03
 
[kube-master]  
BPV-BEF-KBM01  
BPV-BEF-KBM02  
BPV-BEF-KBM03
 
[kube-node]  
BPP-BEF-NODE01  
BPP-BEF-NODE02  
BPP-BEF-NODE03  
BPP-BEF-NODE04  
BPP-BEF-NODE05  
BPP-BEF-NODE06  
BPP-BEF-NODE07
 
[k8s-cluster:children]  
kube-master  
kube-node  
EOF
 
kube 클러스터에 접속 테스트  
$ ansible all -m ping -i ./inventory/op.cfg
 
기본 설치  
$ ansible-playbook -b -i inventory/op.cfg cluster.yml
 
prometheus & grafana 설치  
$ ansible-playbook -b -i inventory/op.cfg monitoring.yml
 
EFK 설치  
$ ansible-playbook -b -i inventory/op.cfg efk.yml
   

설치 후 작업  
각 노드에서 sudo 없이 docker 명령을 사용할 수 있도록 사용자 계정을 docker 그룹에 추가  
$ sudo usermod -aG docker $USER
   

설치 작업 중 발생된 이슈  
- kube-dns pod 등에 crashloopbackoff 발생  
원인: calico가 가상 네트워크를 제대로 구성하지 못하여 각 컴포넌트들이 apiserver에 접근하지 못하여 발생  
해결: calico를 flannel로 대체 후 정상 작동 확인
 
- Prometheus pod이 pending 상태에서 멈춤  
원인: Prometheus pod의 event에서 다음의 메시지 확인  
No nodes are available that match all of the following predicates:: ..... PodToleratesNodeTaints(3)  
해결: prometheus deployment yaml파일에서 NodeSelector를 삭제  
$ kubectl --namespace=kube-system edit deployment prometheus-deployment
      

machine ID 변경  
[http://thegeekdiary.com/centos-rhel-7-how-to-change-the-machine-id/](http://thegeekdiary.com/centos-rhel-7-how-to-change-the-machine-id/)