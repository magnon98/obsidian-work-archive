- ```
    대시보드 UI 아직 반영 안된거라고...
    ```
    
    ```
    html title이 React App으로 출력중. 변경 필요
    ```
    
    - ```
        project 로 필터링 안됨
        ```
        
        ```
        필터하고 summary 하고 무슨 관계인데 보였다 안보였다…?
        ```
        
        - ```
            project 를 모두 선택 해제하면 어떻게 되어야 하나?
            ```
            
            ```
            다시 모두 선택 상태로?
            ```
            
            ```
            아무 것도 안보이기?
            ```
             - ```
    개발 VM 도 MySQL 사용하도록 변경
    ```
    
    ```
    버전: MySQL 5.7
    ```
    
    ```
    database: cpm
    ```
    
    ```
    계정: cpm // 통합포탈1216!
    ```
    
   

```
DB에 밀어넣을 데이터는 init 과정에서 생성? 별도로 쿼리 실행 필요?
```
 
- ```
    [http://183.111.127.201:8080/api/dashboard/org/infra?projects=bliex](http://183.111.127.201:8080/api/dashboard/org/infra?projects=bliex)
    ```
    
    - ```
        조직이 infra 이고 project 가 bliex ???
        ```
        
        ```
        NIA 기준으로 데이터 생성할 필요 있음. 인프라닉스에는 가이드 제공? 우리가 가서 생성?
        ```
        
    - ```
        statistics는 클러스터 전체에 대한 것이 아님.
        ```
        
        - ```
            project에 연결된 namespace의 것만 카운트해야 함.
            ```
            
            ```
            default / ingress-nginx 같은 infra 관련 namespace 를 다 가져오고 있음.
            ```
            
            ```
            클러스터의 모든 namespace를 등록해서 전체가 카운팅된 것???
            ```
            
    - ```
        UI에서 사용되지 않더라도 각 객체의 type, name은 필수로 포함시켰으면
        ```
        
        ```
        데이터만 봐서는 무엇에 대한 것인지 알 수 없음
        ```
        
        ```
        가능하면 parent(?) guid도...
        ```
        

```
### dashboard api
```
 
```
- infranics의 bliex 프로젝트에 클러스터 내의 모든 namespae / space 를 등록한 걸로 보임.  
- statistics의 카운트는 프로젝트에 속한 객체들을 카운트한 것이 맞는지?
```
 
```
- cf는 ingress 가 없어야 하는데... k8s와 동일한 vo? dto? 를 써서 cf 에도 값이 0으로 보이는 것?
```
 
```
- guid c56680d6-f3f4-4284-8167-7252fba8fa5e 인 'cattle-prometheus-p-gnhnm' namespace 에 vm(f7ad6baa-078b-4388-ac85-380c3495a7c0) 이 매핑되어 있는데 vm 목록에서 찾을 수 없음.   
VM의 guid가 맞는지? VM disk는 어떻게 가져온 건지??
```
   

```
- guid 7ef1bdea-494c-4a52-8cb6-802f63f68e80 인 ingress-nginx namespace 에는 deployment 로부터 만들어진 pod 하나에만 request / limit 이 설정되어 있는데 json 에는 값이 2배로 나오고 있음.   
혹시 deployment 와 replicaset 의 값을 합한 것이라면 deployment --\> replicaset --\> pod 로 설정을 상속받는 것이기 때문에 중복 카운팅된 것임.   
deployment 나 replicaset 에서 계산하려면 replica 개수도 고려해야 하므로, 실행중인(Running) pod에서 값을 추출하는 것이 나아보임.
```
 
```
- guid bf9fed98-6de8-4545-b601-08f8fd6c4c14 인 kube-system 에 error 개수가 4개로 잡히는데 이 4개의 status.phase 는 succeeded 로 정상적으로 종료된 pod라서 'succeeded' 인 것은 pod 개수 카운트에서 제외해야 할 것으로 보임
```
 
```
- guid 4f2f1bcf-23a5-43fa-b485-5af5666fc7bb 인 cattle-logging namespace 에 DB VM(guid 203e1032-4d30-407a-b8f0-1d0e38442b9a)이 연결되어 있는데 dashboard api 에는 dbvm.count 값이 0으로 나옴. topology api 에서는 stack에 DB VM이 보임.
```
    
```
### topology api
```
 
```
- pod의 상위 객체(deployment, ***set) 및 service 정보를 확인할 수 없음  
- 좀 더 정확하게는 deployment, service 등의 객체는 있지만  node의 아이템에 type parent 정보 등이 표시되지 않아 node 간 연결을 하기 힘듬.  
- replicaset 에 metadata.ownerReferences 가 있는 경우에는 (거의 대부분 있음) replicaset 을 생략하고 ownerReference인 deployment 만 표현  
즉, deployment  --\> replicaset --\> pod 의 구조이지만 deployment --\> pod 의 구조로 표현
```
 
```
- node 라는 용어가 통합관리자용 토폴로지 데이터 추출시 k8s 노드와 혼동될 가능성 있음.
```
 
```
- stack은 ingress, VM, DB VM 등에 표시할 아이템이 없더라도 빈 배열로 표시하는 것이 명확해 보임.
```
 
```
- ingress가 실제로 있는 'default' namespace(guid: b3a3c8eb-1559-4366-9e76-ec6772b1b111)를 기준으로 조회해도 ingress 가 stack 에 표시되지 않음 
```