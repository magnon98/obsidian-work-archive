reference: [https://kubernetes.io/docs/api-reference/v1.6/](https://kubernetes.io/docs/api-reference/v1.6/)
 
Create Pod  
[https://kubernetes.io/docs/api-reference/v1.6/#create-55](https://kubernetes.io/docs/api-reference/v1.6/#create-55)  
==POST /api/v1/namespaces/{namespace}/pods==  
ex)  
url:  
     [http://localhost:8001/api/v1/namespaces/default/pods](http://localhost:8001/api/v1/namespaces/default/pods)  
header:  
     Content-Type: application/yaml  
payload:  
apiVersion: v1  
kind: Pod  
metadata:  
  name: pod-example  
spec:  
  containers:  
  - name: pod-example  
    image: ubuntu:trusty  
    command: ["echo"]  
    args: ["Hello World"]
 
delete pod  
==DELETE /api/v1/namespaces/{namespace}/pods/{name}==  
ex) [http://localhost:8001/api/v1/namespaces/default/pods/test-nginx](http://localhost:8001/api/v1/namespaces/default/pods/test-nginx)
   

get log  
[https://kubernetes.io/docs/api-reference/v1.6/#read-log](https://kubernetes.io/docs/api-reference/v1.6/#read-log)  
==GET /api/v1/namespaces/{namespace}/pods/{name}/log==