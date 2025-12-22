Amazon Linux를 installer instance로 사용하면 설치가 안됨.  
RHEL에서는 잘 됨.  
Ubuntu16.x, CentOS7 등에서 테스트 필요.
 
모든 노드가 public ip를 가져야 하나??? NO!!!!

- ==Is kubelet started ?====￼====systemctl status kubelet==
- ==Does it schedule containers on Docker====￼====docker ps====￼====journalctl -ae -u kubelet==
- ==Check if the images have been downloaded successfuly====￼====docker images==
 \> 출처: \<[https://github.com/kubernetes-incubator/kubespray/issues/208](https://github.com/kubernetes-incubator/kubespray/issues/208)\>