```
1.     수유 test rmp#no 대상
```

```
rmp02, rmp03
```
  
```
2.     성수 test rmp#no 대상
```

```
rmp02, rmp03
```
  
```
3.     부하 tool 인가 TPS (1st 얼마, 2nd 얼마, 3rd 얼마 등 - 상용이므로 무한정 최대치 불가), delay 수치(우선 stg 시험 때와 동일하게 맞춤)
```

```
TPS 기준로는 설정 불가하여 concurrent user 기준으로 설정
```

```
100 ~ 800 까지 100 또는 200씩 늘려가며 테스트?
```

```
ramp-up 은 stg 와 동일하게 initial 1000, interval 1000 으로 설정
```
  
```
4.     국사별(disk 유형) & host/node 구성별 시험 순서 등
```

```
수유 / 성수 rmp 모두 중단
```

```
수유 rmp 02 기동
```

- ```
    수유 rmp02 단독 테스트 
    ```
    
    ```
     concurrent 얼마로?
    ```
    
    ```
    heap memory - 4GB? 6GB?
    ```
    
    ```
    thread pool size - 기본값으로 한 번, STG 기준 최적값으로 한 번
    ```
    
    ```
    G1GC 
    ```
    

```
수유 rmp02 중단
```

```
수유 rmp03 기동
```

```
수유 rmp03 단독 테스트 - concurrent 얼마로?
```

```
수유 rmp02, rmp03 기동
```

```
수유 rmp02 + rmp03 테스트 - concurrent 얼마로?
```
 
```
수유 / 성수 rmp 모두 중단
```

```
성수 rmp 02 기동
```

```
성수 rmp02 단독 테스트 - concurrent 얼마로?
```

```
성수 rmp02 중단
```

```
성수 rmp03 기동
```

```
성수 rmp03 단독 테스트 - concurrent 얼마로?
```

```
성수 rmp02, rmp03 기동
```

```
성수 rmp02 + rmp03 테스트 - concurrent 얼마로?
```
        
```
5.     측정 툴 준비 (io 관련 fio, dstat 사용 등)
```

```
yum install fio --disablerepo=apigee*
```