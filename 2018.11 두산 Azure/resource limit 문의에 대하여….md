```
request / limit 설정에 대한 정답은 없음.  
어떤 application 을 돌리느냐(언어, 서비스 대상 등)에 따라서 크게 달라질 수 있음.  
클라우드에서도 over provisioning 을 사용하고 있지만, 통계에 기반해서 어느정도까지 가능한지 분석된 결과에 따라 사용중인 것. (인스턴스가 충분히 많아 normalize 가 가능한 수준이라…)  
수 년전 같은 type의 VM인데 성능 격차가 발생한다는 블로그를 본 적도 있음...
```
 
```
DDP 의 경우 인스턴스의 개수가 작아 over provisioning 에 의한 영향도가 크기 때문에 당장은 request / limit을 동일하게 맞춰서 쓰는 것이 안전하고, 어느 정도 사용률에 대한 분석이 진행된 이후 안정적인 over provisioning 비율을 찾아 적용하는 것이 바람직.  
특히 Java Application의 특성상 VM 에서 사용 가능한 메모리의 크기를 XMS, XMX 로 설정해 주어야 하는데 일반적으로 성능을 위해 XMS와 XMX 를 동일한 값으로 설정함. (VM, PaaS 동일)  
( 힙메모리 크기를 늘리는 과정이나 GC 과정에서 일시적으로 성능이 저하됨)  
이 때문에 POD 에서도 request 와 limit을 동일하게 설정하는 경우가 많음.  
XMS, XMX 설정을 다르게 가져가는 경우 request, limit 도 XMS, XMX 값에 맞춰 설정하면 됨.
```
 
```
또는 GC빈도를 크게 늘려 적극적으로 미사용 메모리를 release 하는 방향으로 설정하는 방법도 있음.  
[https://docs.openshift.com/container-platform/3.11/dev_guide/application_memory_sizing.html](https://docs.openshift.com/container-platform/3.11/dev_guide/application_memory_sizing.html)
```
 
```
Pure Java Application 에서는 적절해 보이나, Spring boot 에서도 문제가 없을지는 테스트가 필요함.
```
   

```
리소스를 무조건 많이 할당하기 보다는 stateless 하게 application을 개발하고, 상황에 따라 replica 개수가 늘어날 수 있도록 HPA(auto scale)를 설정하는 것. 리소스를 너무 많이 할당하면 scale out 할 때에도 부담이 됨.
```
   

```
타사의 사례는 레드햇이 제공해줄 수 있을지…  
롯데카드는 on-premise 에 Nutanix VM을 over provisioning 하고, POD는 request == limit 으로 사용.  
Java Application, 2vCPU // 4 ~ 6GiB, Java option에 XMS, XMX 설정. B2C 서비스라서 오픈 후 메모리가 부족하여 하드웨어도 추가 도입되고, 메모리도 추가 할당했다고 나중에 전달받음.  
하드웨어 도입 당시의 예상보다 사용량이 많이 늘게 되어 하드웨어가 부족한 상태.약 PM 별 150 ~ 250% 수준으로 Over provisioning. (Oracle DB, PaaS 를 지원하지 않는 솔루션 등 OCP외에 여러 VM이 있어 가능했던 수치. 오픈 전 수치이며 오픈 후 하드웨어 추가를 통해 더 낮아졌을 것.)
```
 
```
WAS 가 Jboss 라서 scaleout이 오래걸림. POD는 가벼워야 함.
```