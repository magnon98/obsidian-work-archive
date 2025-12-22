```
DEV  
175.113.150.20:9001  
?? // ??
```
 
```
STG  
175.113.150.21:9001  
BG // skbroadband1!
```
    
```
이슈
```

1. ```
    proxy endpoint 와 target endpoint 에 들어갈 내용이 하나의 template 에 혼재되어 있음.
    ```
    
    ```
    template의 구조를 그대로 옮기는 경우 하나의 shared flow로는 처리하기 힘들어 보임.
    ```
    
    2. ```
        단순히 proxy / target endpoint 용의 shared flow를 구분하는 것으로 가능할지?
        ```
        
        ```
        apigee 에 최적화된 shared flow가 되도록 구조가 변경될 필요 있음
        ```
        
      
    
2. ```
    동적으로 백엔드를 변경
    ```
    
    ```
    global variable 또는 local variable 설정에 의해 활성화 
    ```
    
    2. ```
        ex
        ```
        
        ```
        Weighted Routing (A-B 테스트?)
        ```
        
        ```
        특정 셋탑박스 ID는 별도의 Head End를 호출(카나리 테스트?)
        ```
        
        ```
        국사 장애시 다른 국사의 apigee를 호출 (h/e 아님)
        ```
        
      
    
3. ```
    발급된 토큰(authVal)을 DB에 저장해야 함.
    ```
    
    ```
    cassandra 사용? 외부 DB 사용?
    ```
    
    ```
    국사간 데이터 교환은 어떻게??
    ```
    
      
    

```
template을 그대로 옮기려고 하기 보다는 api 설계서? 를 요청해서 비교할 필요
```
 6. ```
    확인되는 global variable은 총 60개. variable들의 의미 / 용도 확인 필요
    ```
    
    ```
    불필요한 것들은 걸러내야...
    ```
     
```
'G2 Encrypt Data', 'G2 Decrypt Data' 와 같은  Custom Assertion 은 내용 확인이 안됨
```
 10.   
    
          
```
주요 로직
```
 
```
- [x] http to https
```

```
- [ ] 헤더 값의 validation check
```

```
- [ ] 국사전환 (국사 상황에 따른 re-routing)
```

```
- [ ] jwt 토큰 검증 - 클라이언트가 셋탑박스가 아닌 경우?
```

```
- [ ] 인증처리 - 인증키(authVal) 검증 및 생성
```

```
- [ ] XSS, SQL Injection 등 대응
```

```
- [ ] data field 암호화 (암호화 로직은 확인 안됨)
```

```
- [ ] a-b 테스트, 카나리 테스트용의 re-routing
```

```
- [ ] 최종 reponse까지 5초 초과시 timeout 처리
```
    

- ```
    국사전환시 프로토콜은 항상 https 가 아닐 수 있는 건지?
    ```
    
    ```
    L4 / L7에서 TLS termination 하는거면 apigee는 항상 http로만 호출될텐데?
    ```
    
    ```
    protocol / port 확인을 위해 x-forwarded-proto 나 x-forwarded-port 를 확인해야 하는건가?
    ```
     
```
국사전환의 audit log 에 ${httpRouting.reasonCode} 는 어떤 변수인지?￼
```

```
헤더 세팅에 보면 8090 포트인 경우 분기처리가 있는데 8090은 어떤 포트?￼
```

```
audit log 및 ELK 로깅에서 ${targetURL} 값을 출력하도록 되어 있는데 아직 H/E 를 호출하기 전이기 때문에 H/E 의 IP를 알 수 없음.￼targetURL 이 H/E 가 아닌 STB가 호출하는 URL을 말하는건지?￼
```

```
API Key 확인 (100.33.12) 에서 oauth_consumer_key 가 사용되는데 출처를 알 수 없음.
```
 
```
${service.oid}는 CA 에서는 uuid 형태로 제공되지만, Apigee 에서는 uuid 형태로 제공되지 않음.￼개별 API를 구분하기 위해 사용되는 것으로 보이는데 unique한 값이면 uuid 형태가 아니어도 되는지?￼필요하다면 각 API에 uuid 값을 지정할 수는 있음.￼
```

- ```
    비활성화된 코드들을 분석해보면 불완전한 설정들이 상당수 보이는데 최대한 비슷하게 구현하고 비활성화시키면 될지?
    ```
    
    ```
    순서가 바뀐 코드 (변수 사용 후 변수 할당 등)
    ```
    
    ```
    선언했지만 사용하지 않는 변수
    ```
    
    ```
    동일한 조건문 - 다른 설정의 반복 (100.33.34.9, 100.33.34.27, 100.33.34.45)
    ```
    
    ```
    빈 string 에 대한 split 시도￼
    ```
    

```
${controll.590} 은 cluster-wide 또는 local 변수인지, 아니면 CA 가 제공하는 객체인지?
```
 -