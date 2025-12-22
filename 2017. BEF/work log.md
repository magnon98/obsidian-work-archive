[https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/#network-traffic-is-not-forwarded](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/#network-traffic-is-not-forwarded)
 
```
/home/magnon/backups/kubespray.old/roles/kubernetes/node/templates/kubelet.j2  
16라인에 아래 내용 추가  
--hairpin-mode=promiscuous-bridge \
```

[https://stackoverflow.com/questions/41479648/kubernetes-networking-issue-service-nodeport-cant-be-reached-externally/41564282#41564282](https://stackoverflow.com/questions/41479648/kubernetes-networking-issue-service-nodeport-cant-be-reached-externally/41564282#41564282)
 
Iptable 문제. FORWARD를 ACCEPT로 변경하는 방법