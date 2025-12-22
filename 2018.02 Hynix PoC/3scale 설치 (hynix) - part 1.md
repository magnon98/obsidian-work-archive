==인스턴스== ==생성==  
==아래의== ==스펙으로== ==XenServer====에== ==인스턴스== ==생성====.==

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
|**용도**|**hostname**|**CPU (#)**|**RAM (GB)**|**Storage (GB)**|**OS**|**IP Addr**|
|DNS 서버|3scale-ose-dns|2|4|50|CentOS 7.4|192.168.100.40|
|Master|m1.example.com|2|8|50|RHEL 7.4|192.168.100.41|
|Infra|i1.example.com|2|8|50|RHEL 7.4|192.168.100.42|
||i2.example.com|2|8|50|RHEL 7.4|192.168.100.43|
|Node|w1.example.com|2|8|50|RHEL 7.4|192.168.100.44|
||w2.example.com|2|8|50|RHEL 7.4|192.168.100.45|

==RHEL== ==설치== ==후== ==subscription== ==등록==  

```
$ sudo subscription-manager register --username=redhat@exntu.com --password=exntu~redhat --auto-attach
$ sudo subscription-manager list --available --matches '*OpenShift*'          ### 
```

출력 결과에서 `Pool ID` 값 확인  
`$ sudo subscription-manager attach --pool=8a83f98c61acd5bf0161ad5f92d70ac1`  
   
==sudoer====에== ==NOPASSWD== ==설정==  

```
$ echo -e $USER"\tALL=(ALL)\tNOPASSWD: ALL" | sudo tee -a /etc/sudoers
```
    
==OS== ==업데이트== ==및== ==필수== ==유틸== ==사전== ==설치==  

```
$ sudo yum install -y wget git net-tools bind-utils iptables-services bridge-utils bash-completion vim
$ sudo yum update -y
$ reboot
$ sudo yum remove kernel        ### 
```

구버전 커널 제거  
   
==DNS== ==서버== ==설정==  
**bind, bind-utils** **패키지** **설치**  

```
$ sudo yum install bind bind-utils
$ sudo systemctl enable
```
    
**named.conf** **설정** **변경**  

```
$ sudo vi /etc/named.conf
### options 
```

하위의 `listen-on` 과 `allow-query`의 괄호안의 값을 `any`로 변경  

```
...
options {
...
    listen-on port 53 { any; };
...
...
    allow-query       { any; };
...
...
}
...
...
include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";
### 
```

내부 `DNS`를 관리하는 `zone`에 대한 설정파일 추가  

```
include "/etc/named.conf.local";
```
    
**/etc/named.conf.local**  

```
zone "example.com" {
    type master;
    file "/etc/named/zones/db.example.com";
};
 
zone "100.168.192.in-addr.arpa" {
    type master;
    file "/etc/named/zones/db.192.168.100";
};
```
    
**/etc/named/zones/db.example.com**  

```
$TTL    604800
@       IN      SOA     ns1.example.com. ns2.example.com. (
                  3     ; Serial
             604800     ; Refresh
              86400     ; Retry
            2419200     ; Expire
             604800 )   ; Negative Cache TTL
;
; name servers - NS records
     IN      NS      ns1.example.com.
     IN      NS      ns2.example.com.
; name servers - A records
ns1.example.com.         IN      A      192.168.100.40
ns2.example.com.         IN      A      192.168.100.39
; 192.168.100.0/24 - A records
m1.example.com.          IN      A      192.168.100.41
i1.example.com.          IN      A      192.168.100.42
i2.example.com.          IN      A      192.168.100.43
w1.example.com.          IN      A      192.168.100.44
w2.example.com.          IN      A      192.168.100.45
apps.example.com.        IN      A      192.168.100.42
apps.example.com.        IN      A      192.168.100.43
amp.example.com.         IN      A      192.168.100.42
amp.example.com.         IN      A      192.168.100.43
*.apps.example.com.      IN      A      192.168.100.42
*.apps.example.com.      IN      A      192.168.100.43
*.amp.example.com.       IN      A      192.168.100.42
*.amp.example.com.       IN      A      192.168.100.43
```
   

**/etc/named/zones/db.192.168.100**  

```
$TTL    604800
@       IN      SOA     example.com. ns1.example.com. (
                              3         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
; name servers
      IN      NS      ns1.example.com.
      IN      NS      ns2.example.com.
; PTR Records
40.100    IN      PTR     ns1.example.com.    ; 192.168.100.40
39.100    IN      PTR     ns2.example.com.    ; 192.168.100.39
41.100    IN      PTR     m1.example.com.     ; 192.168.100.41
42.100    IN      PTR     i1.example.com.     ; 192.168.100.42
43.100    IN      PTR     i2.example.com.     ; 192.168.100.43
44.100    IN      PTR     w1.example.com.     ; 192.168.100.44
45.100    IN      PTR     w2.example.com.     ; 192.168.100.45
42.100    IN      PTR     apps.example.com.   ; 192.168.100.42
43.100    IN      PTR     apps.example.com.   ; 192.168.100.43
42.100    IN      PTR     amp.example.com.    ; 192.168.100.42
43.100    IN      PTR     amp.example.com.    ; 192.168.100.43
```
   

**named** **설정** **검사**  

```
$ sudo named-checkconf /etc/named.conf.local
$ sudo named-checkzone example.com /etc/named/zones/db.example.com
zone example.com/IN: loaded serial 3
OK
$ sudo named-checkzone 100.168.192.in-addr.arpa /etc/named/zones/db.192.168.100
zone 100.168.192.in-addr.arpa/IN: loaded serial 3
OK
```
   

**named** **서비스** **자동실행** **설정** **/** **시작**  
`###` 방화벽 해제  

```
$ sudo systemctl stop firewalld
$ sudo systemctl disable firewalld
 
 
### 
```

서비스 등록 및 시작  

```
$ sudo systemctl enable named
$ sudo systemctl start named 
$ systemctl status named
 
### 
```

테스트  

```
$ nslookup m1.example.com 127.0.0.1
```
    
==Openshift== ==용== ==인스턴스의== ==네트워크== ==설정== ==변경==  
==resolv.conf== ==에== ==search== ==키워드로== ==cluster.local== ==및== ==svc.cluster.local== ==이 등록되어 있어야== ==￼====내부 서비스 도메인== ==(docker-registry.default.svc== ==등====)====을 사용할 수 있음==  
==resolv.conf====는== ==NetworkManager== ==에== ==의해== ==자동생성되므로====,== ==직접== ==수정하는== ==대신== ==NIC== ==설정을== ==변경해야== ==함====.==
 
**/etc/sysconfig/network-scripts/ifcfg-xxx**  
`###` 아래 내용 추가`.` 중복항목은 제거 또는 병합  

```
DOMAIN="cluster.local svc.cluster.local"
DNS1=192.168.100.40
DNS2=8.8.8.8
DNS3=8.8.4.4
```
    
==Ansible== ==머신== ==구성==  
**openshift-ansible** **설치**  
`### Python, pip` 설치  

```
$ which pip || sudo yum install -y python2-pip
$ sudo pip install --upgrade pip
 
### ansible 
```

설치  

```
$ sudo pip install ansible
 
### openshift ansible 
```

다운로드  

```
$ git clone https://github.com/openshift/openshift-ansible.git
```
   

**inventory/3scale.cfg**   

```
# referenced url: https://www.snip2code.com/Snippet/2576082/Openshift-inventory-with-HA-multi-master/
# ansible all --module-name=ping --inventory=inventory/3scale.cfg
# ansible-playbook --inventory=inventory/3scale.cfg ./playbooks/
```

byo/config

```
.yml
# ansible-playbook --inventory=inventory/3scale.cfg ./playbooks/adhoc/uninstall.yml
 
m1.example.com ansible_host=192.168.100.41 ansible_port=22
i1.example.com ansible_host=192.168.100.42 ansible_port=22
i2.example.com ansible_host=192.168.100.43 ansible_port=22
w1.example.com ansible_host=192.168.100.44 ansible_port=22
w2.example.com ansible_host=192.168.100.45 ansible_port=22
 
[masters]
m1.example.com
 
[etcd]
m1.example.com
 
[nodes]
i1.example.com openshift_node_labels="{'region': 'infra'}"
i2.example.com openshift_node_labels="{'region': 'infra'}"
w1.example.com
w2.example.com
 
[OSEv3:children]
masters
nodes
 
[OSEv3:vars]
### ansible ssh account info
ansible_ssh_user=bliex
ansible_ssh_private_key_file=/home/magnon/.ssh/vm_rsa
ansible_become=true
 
#openshift_dns_ip=192.168.100.40
openshift_use_dnsmasq=true
 
### OpenShift Version
#deployment_type=origin
deployment_type=openshift-enterprise
openshift_deployment_type=openshift-enterprise
 
# 3.6.173.0.96
openshift_release=v3.6
# openshift_upgrade_target=3.6
# openshift_image_tag=v3.6.0
# openshift_pkg_version="-3.6"
 
### Fix not meet requirement
openshift_disable_check=docker_storage,docker_image_availability,memory_availability
# openshift_disable_check=docker_storage,memory_availability,disk_availability
 
### Native HA
openshift_master_cluster_method=native
openshift_master_cluster_hostname=m1.example.com
openshift_master_cluster_public_hostname=m1.example.com
openshift_master_default_subdomain=apps.example.com
#openshift_master_portal_net=10.100.0.0/16
 
### misc. settings...
openshift_node_kubelet_args={'pods-per-core': ['10'], 'max-pods': ['250'], 'image-gc-high-threshold': ['90'], 'image-gc-low-threshold': ['80']}
openshift_clock_enabled=true
openshift_hosted_registry_selector='region=infra'
```
   

**ansible ping** **테스트**  
`# ansible all --module-name=ping --inventory=inventory/3scale.cfg`
   

**Openshift Enterprise** **설치**  
`# ansible-playbook --inventory=inventory/3scale.cfg ./playbooks/`byo/config`.yml`
   

**Openshift** **삭제**  
`# ansible-playbook --inventory=inventory/3scale.cfg ./playbooks/adhoc/uninstall.yml`  
   
==설치== ==후속작업==  
==웹콘솔에서의== ==계정== ==생성이== ==막혀== ==있어== ==테스트용으로== ==적합하지== ==않음====.==  
==입력받는== ==ID /== ==비밀번호로== ==자동생성하도록== ==DenyAllPasswordIdentityProvider====을== ==찾아== ==AllowAllPasswordIdentityProvider== ==로== ==변경==
   

**/etc/origin/master/master-config.yaml**  

```
...
...
oauthConfig:
  assetPublicURL: https://m1.example.com:8443/console/
  grantConfig:
    method: auto
  identityProviders:
  - challenge: true
    login: true
    mappingMethod: claim
#    name: deny_all
    name: allow_all
    provider:
      apiVersion: v1
#     kind: DenyAllPasswordIdentityProvider
      kind: AllowAllPasswordIdentityProvider
...
... 
```
   

**마스터** **노드** **재시작**  

```
$ sudo systemctl restart atomic-openshift-master 
```
    
==https://m1.example.com:8443====에 접속해서 계정 생성 및 테스트==