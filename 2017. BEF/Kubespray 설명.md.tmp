Network plugin 변경  
Kubespray/inventory/group-vars/k8s-cluster.yml 에서 다음을 변경
 
```
# Choose network plugin (calico, weave or flannel)  
# Can also be set to 'cloud', which lets the cloud provider setup appropriate routing  
kube_network_plugin: calico
```
 
Kubespray/roles/kubespray-defaults/defaults/main.yaml 에도 동일한 값이 있으나 k8s-cluster.yml에 의해 override됨.
 
경험상 장비 사양 및 H/W 에 따라 특정 네트워크 플러그인이 정상 작동을 하지 않는 경우가 있음.

Worker Node의 nginx  
api 서버에 쉽게 접근할 수 있도록 각각의 worker node에 nginx를 이용한 reverse proxy가 생성됨.
 
```
error_log stderr notice;
```
 
```
worker_processes auto;  
events {  
  multi_accept on;  
  use epoll;  
  worker_connections 1024;  
}
```
 
```
stream {  
        upstream kube_apiserver {  
            least_conn;  
            server 223.39.117.60:6443;  
            server 223.39.117.61:6443;  
            server 223.39.117.62:6443;  
        }
```
 
```
        server {  
            listen        127.0.0.1:6443;  
            proxy_pass    kube_apiserver;  
            proxy_timeout 10m;  
            proxy_connect_timeout 1s;  
        }  
}
```

클러스터에 노드 추가 (non-master 노드만 가능)

1. Inventory 파일( kubespray/inventory/op.cfg )에 노드 추가
2. --limit 옵션으로 추가할 노드를 지정하여 설치 스크립트 실행
3. 노드 목록 확인

```
$ ansible-playbook -b -i inventory/op.cfg cluster.yml --limit [node-name]  
$ kubectl get node
```

VM shutdown / startup / reboot  
마스터 및 워커 노드에 대한 별도의 작업은 필요치 않음.  
다만 워커 노드를 shutdown하는 경우 실행중인 pod의 특성에 따라 정보 유실 우려가 있으므로 정보 저장이 필요한 pod에 대해서는 별도의 절차 필요.
 
클러스터에서 노드 삭제  
kubectl을 사용해서 제거  
$ kubectl delete node [node-name]