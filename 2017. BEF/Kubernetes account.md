K8s-cluster.yml
 
```
kube_api_pwd: "{{ lookup('password', 'credentials/kube_user length=15 chars=ascii_letters,digits') }}"  
kube_users:  
  kube:  
    pass: "{{kube_api_pwd}}"  
    role: admin  
    groups:  
      - system:masters  
  user_id:  
    pass: "user_passwd"  
    role: …..  
    groups:  
      - ……
```