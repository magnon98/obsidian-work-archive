```
- [ ] PVC로 마운트되는 볼륨에서 특정 user, group, permission이 필요한 경우 mount 전에 PVC를 생성하고, 같이 생성된 PV에 uid, gid, permission 등을 설정 (PV 의 mountOptions 속성 참조)  
- [ ] 두산 SSO 설정을 위해 Kerberos 를 사용.￼AD 에서 keytab 발급이 필요. 신규 도메인 추가시 SPN 등록 필요.  
- [ ] OCP에 htpasswd 방식의 계정 추가는 모든 마스터에 빠짐없이  
- [ ] App Node 에서의 Outbound IP는 52.231.79.32  
- [ ] Azure AD 에서 Kerberos 인증을 사용하려면 Azure AD Domain Service 가 추가로 필요  
- [ ] 3Scale API 의 Kerberos 인증은 Fuse(apig-custom) 에서 처리  
- [ ] Kerberos 인증 때문에 각 노드는 authsj.corp.doosan.com 를 resolve 할 수 있어야 함. (현재는 hosts 에 등록)  
- [ ] RWO PVC를 사용하는 DC 는 update strategy 를 Rolling 이 아닌 Recreate 로  
- [ ] RWX 가 필요한 경우 storage class 는 azurefile로  
- [ ] 각 노드에 prune script 있음. ddp-master-01에는 integrated registry 에 대한 pruning 도 들어 있음.  
- [ ] 3scale 의 wildcard router 는 1MB 업로드 제한, 업로드 용량 제한은 application 에서 (WAF 도 가능?)
```