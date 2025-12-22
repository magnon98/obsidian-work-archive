# KVM
 
```
AuthTokens  
토큰 저장용 내부 DB  
Put-Token apiproxy에서 토큰 저장.  
SF-Authorization-and-Traffic-Control 에서 토큰 사용  
RDB 사용하는 것으로 변경
```
 
```
CDB_Account  
CDB 접속정보 저장 (id, pw, url …)
```
 
```
Gateway  
국사별 apigee 설정 (
```
 
```
JWT  
JWT 생성 / 검증을 위한 HMAC secret 저장  
9fcf2f03-44ac-4389-bd4a-6e51c121365c=eb71dc16-2160-434c-a2d6-76ea11c3450b
```
 
```
TokenPushCredentials  
Get-Token / Put-Token API 에서 사용
```
   

```
apiKeyRecords  
apiproxy 별로 apiKey 등록하기 위해 사용
```

# Cache
 
```
MacCache  
Get-Token apiproxy의 SF-Issue-Token 에서 mac addr 캐시
```
   

```
TokenCache  
최근 사용 토큰 저장용 캐시
```