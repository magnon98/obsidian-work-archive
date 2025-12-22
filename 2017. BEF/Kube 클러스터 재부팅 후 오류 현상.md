노드쪽의 에러에 docker-storage-setup 관련 에러가 보임.  
docker 1.12까지 있던 실행파일이지만, 1.13 이후 삭제된 파일로 보임.
 
```
$ sudo yum provides docker-storage-setup
```
   

Flannel -\> calico, docker 1.13 --\> 17.03으로 변경 후  
노드를 한 개씩 재부팅하는 경우 정상적으로 복구되나  
모두 power-off한 경우 worker node가 복구되지 않음.  
Nginx 가 upstream을 찾지 못해 kubelet이 클러스터에 가입하지 못하는 것으로 보임.