[https://kubernetes.io/docs/tasks/administer-cluster/cpu-memory-limit/](https://kubernetes.io/docs/tasks/administer-cluster/cpu-memory-limit/)  

```
$ cat \<\< EOF \> mylimits.yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: mylimits
spec:
  limits:
  - max:
      cpu: "2"
      memory: 1Gi
    min:
      cpu: 200m
      memory: 6Mi
    type: Pod
  - default:
      cpu: 300m
      memory: 200Mi
    defaultRequest:
      cpu: 200m
      memory: 100Mi
    max:
      cpu: "2"
      memory: 1Gi
    min:
      cpu: 100m
      memory: 3Mi
    type: Container
EOF
$ kubectl create -f mylimits.yaml --namespace=XXX
$ kubectl describe limits mylimits --namespace=XXX
```
   

```
roles/kubernetes/master/defaults/main.yml
    kube_apiserver_memory_limit: 512M
roles/kubernetes/node/defaults/main.yml
    kube_proxy_memory_limit: 512M
```