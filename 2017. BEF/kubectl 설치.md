```
$ kubectl config set-cluster master1 \  
--certificate-authority=/home/suser/ssl/ca.pem \  
--embed-certs=true \  
--server=https://223.39.117.60:6443
```
 
```
서버 주소는 master의 것 또는 master를 가리키는 reverse proxy로.
```

```
$ kubectl config set-credentials admin \  
--client-certificate=/home/suser/ssl/apiserver.pem \  
--client-key=/home/suser/ssl/apiserver-key.pem
```
 
```
$ kubectl config set-context master1 \  
--cluster=master1 \  
--user=admin
```
 
```
$ kubectl config use-context master1
```
   

```
$ kubectl get componentstatuses
```