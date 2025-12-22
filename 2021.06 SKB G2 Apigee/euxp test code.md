```
curl -v '[http://10.10.214.114/euxp/v5/menu/gnbBlock?IF=IF-EUXP-030&stb_id=%7B660D7F55-89D8-11E5-ADAE-E5AC4F814417%7D&seg_id=&version=&menu_stb_svc_id=BTVMOBV521&app_typ_cd=BTVPLUS](http://10.10.214.114/euxp/v5/menu/gnbBlock?IF=IF-EUXP-030&stb_id=%7B660D7F55-89D8-11E5-ADAE-E5AC4F814417%7D&seg_id=&version=&menu_stb_svc_id=BTVMOBV521&app_typ_cd=BTVPLUS)' \  
    -H 'Host: agw2.skbroadband.com' \  
    -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNjI2ODUxODMzLCJleHAiOjE2NTg4NTE4MzN9.cJJbNhjrUpuMTYeXHUtOz_hfSTQUhUedFLLFjOlAv7o' \  
    -H 'Client_ID: 660D7F55-89D8-11E5-ADAE-E5AC4F814417' \  
    -H 'Api_Key: l7xx159a8ca72966400b886a93895ec9e2e3' \  
    -H 'Timestamp: 20210805123456.789' \  
    -H 'Auth_Val: 1f0f745b4a4550c9da5dd74473eb6bcb0221ec5c4aa53d137e3ea7d78528908c' \  
    -H 'Trace: DEV^APIGEE|1628173713652^TOKENIDPS'
```
       
```
access token은 HMAC secret을 이용해서 임의로 생성한 값을 사용.
```
 
```
Client ID 는 PoC에서 euxp 호출시 사용하던 값을 사용  
querystring 의 stb_id 와는 중복인 건데, 이게 맞는지?  
셋탑박스가 호출할 때에는 Header에만 값이 있고, Apigee 에서 querystring에 추가하는 건지?
```
 
```
Client ID 와 매핑되는 Token 값은 테스트를 위해 KVM에 수동으로 임의의 값을 등록  
실사용시에는 CA 에서 기 등록된 값을 추출하여 Apigee 에 밀어넣어야 함.
```
 
```
Timestamp 는 Unix Timestamp 가 아닌 datetime인 건지?
```