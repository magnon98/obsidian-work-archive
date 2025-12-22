```
Kubernetes Engine API  활성화
```

![Google Cloud Platform DentalinkAllStaging Kubernet...](Exported%20image%2020251106120212-0.png)   
```
k8s 클러스터 생성
```

![Kubernetes Engine Kubernetes clusters Containers p...](Exported%20image%2020251106120214-1.png)  
![Create cluster Select the cluster mode that want t...](Exported%20image%2020251106120216-2.png)   ![Google Cloud Platform DentalinkAllstaging Search p...](Exported%20image%2020251106120217-3.png)   ![Google Cloud Platform DentalinkAllstaging Search p...](Exported%20image%2020251106120224-4.png)         
```
$ gcloud config configurations create pms-stg
```
 
```
$ gcloud config set account magnon@bliex.com  
$ gcloud config set project dentalinkall-staging  
$ gcloud config set compute/region asia-northeast3  
$ gcloud config set compute/zone asia-northeast3-a
```
 
```
$ gcloud config configurations activate pms-stg
```
 
```
$ gcloud container clusters get-credentials pms-stg-cluster-1
```