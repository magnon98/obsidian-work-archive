```
AUTH_TOKEN=`kubectl get secret $TOKEN_NAME -o jsonpath='{.data.token}' | base64 -d`  
echo -e `kubectl get serviceaccount default -o json | jq ".secrets[].name"`  
echo -n `kubectl get serviceaccount default -o json | jq ".secrets[].name"`  
echo `kubectl get serviceaccount default -o json | jq ".secrets.name"`  
echo `kubectl get serviceaccount default -o json | jq ".secrets[].name"`  
kubectl cluster-info  
kubectl cluster-info dump  
kubectl cluster-info dump \> cluster_info_dump  
kubectl config  
kubectl config set-credentials --help  
kubectl config set-credentials --help | more  
kubectl config set-credentials admin --client-certificate=~/admin_ca.crt --embed-certs=true  
kubectl config set-credentials admin --token=" =="  
kubectl config set-credentials help  
kubectl config view  
kubectl config view -o json  
kubectl config view -o jsonpath ".users"  
kubectl config view -o jsonpath="..users"  
kubectl config view -o jsonpath=".users"  
kubectl config view -o jsonpath="{.users[*].name}"  
kubectl config view -o jsonpath="{.users}"  
kubectl config view -o jsonpath='{.users[*].user.token}'  
kubectl config view -o jsonpath='{.users[*].user.token}' | base64 -id  
kubectl config view -o jsonpath='{.users[?(@.name=="admin")].user.token}'  
kubectl config view -o jsonpath='{.users[?(@.name=="admin")].user.token}' | base64 -d  
kubectl config view -o jsonpath='{.users[?(@.name=="admin")]}'  
kubectl create -f dashboard.yaml  
kubectl create -f role.yaml  
kubectl create serviceaccount jh  
kubectl describe kube-apiserver-master01 --namespace=kube-system  
kubectl describe kubernetes-dashboard-2396447444-5khpx  
kubectl describe pod  
kubectl describe pod --all-namespaces  
kubectl describe pod --all-namespaces | grep -i "Name:"  
kubectl describe pod --all-namespaces | more  
kubectl describe pod flannel --all-namespaces  
kubectl describe pod flannel-master01 --namespace=kube-system  
kubectl describe pod kube-apiserver-master01 --namespace=kube-system  
kubectl describe pod kube-proxy-worker02 --all-namespaces  
kubectl describe pod kubernetes-dashboard-2396447444-5khpx --namespace=kube-system | more  
kubectl describe pod test-nginx  
kubectl describe pods  
kubectl describe pods | grep -i "172.16."  
kubectl describe pods/kube-apiserver-master01  
kubectl describe pods/kube-apiserver-master01 --namespace=kube-system  
kubectl describe secrets/default-token-c4nn6  
kubectl describe secrets/default-token-c4nn6 -o yaml  
kubectl describe service/kubernetes  
kubectl describe service/kubernetes -o yaml  
kubectl describe services kubernetes-dashboard --namespace=kube-system  
kubectl describe services/kubernetes  
kubectl exec --help  
kubectl exec flannel-master01 --namespace=kube-system ls  
kubectl exec flannel-master01 ls  
kubectl exec kube-proxy-master01 --namespace=kube-system /bin/sh  
kubectl exec test-nginx which nginx  
kubectl expose --help  
kubectl get deployment  
kubectl get deployment --all-namespaces  
kubectl get deployment -o wide  
kubectl get deployment -o wire  
kubectl get expose  
kubectl get ingress --all-namespaces  
kubectl get ingresses --all-namespaces  
kubectl get pod  
kubectl get pod --all-namespaces  
kubectl get pod --all-namespaces | grep master  
kubectl get pod --all-namespaces | grep worker  
kubectl get pods  
kubectl get pods --all-namespaces  
kubectl get pods --all-namespaces -o wide  
kubectl get pods --all-namespaces -o wide | grep "10."  
kubectl get pods --all-namespaces | grep dashboard  
kubectl get pods -o wide  
kubectl get pods -o yaml  
kubectl get pods/hello-3571968426-xhbb0  
kubectl get pods/hello-3571968426-xhbb0 -o yaml  
kubectl get pods/kubernetes-dashboard-2396447444-5khpx --namespace=kube-system -o json  
kubectl get pods/kubernetes-dashboard-2396447444-5khpx --namespace=kube-system -o json | jq ".spec.serviceAccount"  
kubectl get pods/kubernetes-dashboard-2396447444-5khpx --namespace=kube-system -o jsonfilter  
kubectl get pods/kubernetes-dashboard-2396447444-5khpx --namespace=kube-system -o jsonformat  
kubectl get pods/kubernetes-dashboard-2396447444-5khpx --namespace=kube-system -o yaml  
kubectl get pods/kubernetes-dashboard-2396447444-5khpx -o yaml  
kubectl get role  
kubectl get role --all-namespaces  
kubectl get rolebinding  
kubectl get rolebinding --all-namespaces  
kubectl get secret $TOKEN_NAME  
kubectl get secret $TOKEN_NAME -o json | jq ".data.token" | base64 -id  
kubectl get secret $TOKEN_NAME -o jsonpath='{.data.token}'  
kubectl get secret $TOKEN_NAME -o jsonpath='{.data.token}' | base64 -d  
kubectl get secret $TOKEN_NAME -o jsonpath='{.data}'  
kubectl get secret $TOKEN_NAME -o yaml  
kubectl get secret admin-token-8ngzl -o yaml  
kubectl get secret default-token-c4nn6 -o json  
kubectl get secret default-token-c4nn6 -o json | jq ".data.token"  
kubectl get secret default-token-c4nn6 -o json | jq ".data.token" | base64 --decode  
kubectl get secret default-token-c4nn6 -o json | jq ".data.token" | base64 --di  
kubectl get secret default-token-c4nn6 -o json | jq ".data.token" | base64 -id  
kubectl get secret default-token-c4nn6 -o yaml  
kubectl get secret jh -o yaml  
kubectl get secret jh-token-5bdcl -o yaml  
kubectl get secret/admin  
kubectl get secrets  
kubectl get secrets admin  
kubectl get secrets admin-token-8ngzl  
kubectl get secrets admin-token-8ngzl -o json  
kubectl get secrets/admin  
kubectl get service  
kubectl get service --all-namespaces  
kubectl get service -o wide  
kubectl get service/kubernetes -o yaml  
kubectl get serviceaccoun/t/default  
kubectl get serviceaccount  
kubectl get serviceaccount --all-namespaces  
kubectl get serviceaccount admin -o yaml  
kubectl get serviceaccount default  
kubectl get serviceaccount default -o json  
kubectl get serviceaccount default -o json | jq ".secrets.name"  
kubectl get serviceaccount default -o json | jq ".secrets[].name"  
kubectl get serviceaccount default -o json | jq ".secrets[].name"  
kubectl get serviceaccount default -o jsonpath="{.secrets..name}"  
kubectl get serviceaccount default -o jsonpath="{.secrets..name}"  
kubectl get serviceaccount default -o jsonpath="{.secrets}"  
kubectl get serviceaccount default -o yaml  
kubectl get serviceaccount degault  
kubectl get serviceaccount jh -o yaml  
kubectl get serviceaccount/admin  
kubectl get serviceaccount/admin --all-namespaces  
kubectl get serviceaccount/default  
kubectl get serviceaccount/default -o json  
kubectl get serviceaccount/default -o yaml  
kubectl get serviceaccount/jh  
kubectl get serviceaccount/jh -o yaml  
kubectl get services --all-namespaces  
kubectl get services/kubernetes  
kubectl get status  
kubectl get status --all-namespaces  
kubectl log hello  
kubectl log services/kubernetes  
kubectl logs  
kubectl logs --help  
kubectl logs flannel-master01  
kubectl logs flannel-master01 --namespace=kube-system  
kubectl logs flannel-worker01 --namespace=kube-system  
kubectl logs flannel-worker02 --namespace=kube-system  
kubectl logs hello  
kubectl logs hello-3571968426-xhbb0  
kubectl logs kube-apiserver-master01  
kubectl logs kube-apiserver-master01 --namespace=kube-system  
kubectl logs kube-apiserver-master02 --namespace=kube-system  
kubectl logs nginx-2371676037-49503 nginx  
kubectl logs po  
kubectl logs pod  
kubectl logs pod-example  
kubectl logs pods  
kubectl logs services/kubernetes  
kubectl logs test-nginx  
kubectl pod describe kubernetes-dashboard-2396447444-5khpx  
kubectl port-forward --help  
kubectl proxy  
kubectl proxy &  
kubectl top node  
kubectl top node --namespace=default  
kubectl top pod
```