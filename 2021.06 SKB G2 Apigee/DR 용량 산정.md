```
RMP 노드의 개수는 RMP 노드당 2000 tps 로 계산.
```
   

```
2KB/req, 20,000tps, 하루 24시간, 30일 보관시 postgresql 용량
```
 
```
A   (# bytes of analytics data/request) *	                   2,048   
B   (requests/second) *	                                    20,000   
C   (seconds/hour) *                                         3,600   
D   (hours of peak usage/day) *                                 24   
E   (days of data retention)	                                 30  
----------------------------------------------------------------------  
G   bytes (A * B * C * D * E * F) 	           106,168,320,000,000   
----------------------------------------------------------------------  
    tera bytes (G / 2^40) 		                 96.56
```
       
```
2KB/req, 20,000tps, 하루 8시간, 30일 보관시 postgresql 용량
```
 
```
A   (# bytes of analytics data/request) *	                   2,048   
B   (requests/second) *	                                    20,000   
C   (seconds/hour) *                                         3,600   
D   (hours of peak usage/day) *                                  8   
E   (days of data retention)	                                 30  
----------------------------------------------------------------------  
G   bytes (A * B * C * D * E * F) 	            35,389,440,000,000   
----------------------------------------------------------------------  
    tera bytes (G / 2^40) 		                 31.19
```

```
Postgresql은 RDS 사용하는 방법과 EC2 인스턴스를 사용하는 방법이 있음.
```
 
- ```
    Postgresql 스토리지의 최대 크기는 64TiB
    ```
    
    - ```
        RDS 사용시 64 TiB 한도로 Storage autoscaling 사용 가능
        ```
        
        - ```
            autoscaling 6시간에 한 번만 작동 가능하므로 6 ~ 7시간 분량의 데이터 (약 0.8 ~ 0.94 TiB) 가 스토리지 크기의 10% 미만이어야 함.
            ```
            
            ```
            스토리지 최소 사이즈를 10 TiB 이상으로 설정 필요.
            ```
            
        
        ```
        scaleout된 스토리지는 줄일 수 없음.
        ```
        
        - ```
            RDS 사용시 postgres-server, qpidd, qpidd-server 를 위한 인스턴스는 여전히 필요하지만
            ```
            
            ```
            이 인스턴스의 스펙을 결정하기 위한 근거가 
            ```
            
    - ```
        EC2 인스턴스 사용시
        ```
        
        ```
        EBS 단일 볼륨의 최대 크기가 16 TiB (LVM 2.0의 제약사항)
        ```
        
        - ```
            storage autoscaling 사용 불가
            ```
            
            ```
            LVM을 사용하여 스토리지 사용량 모니터링 및 볼륨 확장 필요.
            ```
            
            ```
            RDS 의 autoscaling 6시간 제한이 없으므로 더 작은 단위로 용량 증설 가능
            ```
            
        
        ```
        Multi-AZ 기능을 사용할 수 없으므로 이중화 구성 필요
        ```
        
          
        
   

- ```
    SSD GP2 볼륨의 최대 IOPS 는 5.34 TiB 이상에서 16,000 IOPS
    ```
    
    ```
    스토리지 최소 크기를 5.5TiB 이상으로 설정 필요
    ```
    
    ```
    3,000 IOPS 를 초과하므로 Burst 대상이 아님.
    ```
    
   

- ```
    참조 링크
    ```
    
    ```
    [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTpes.html#USER_PIOPS.Autoscaling](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTpes.html#USER_PIOPS.Autoscaling)
    ```
    
    ```
    [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html#Concepts.Storage.GeneralSSD](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Storage.html#Concepts.Storage.GeneralSSD)
    ```
    

|
|
```
SKB  하루 평균 트래픽
```
```
8억건
```
```
DR 목표 트래픽
```
```
20,000 TPS
```
```
busy hour
```
```
8억 / 20000 / 3600 ≒ 11.111111
```
|||