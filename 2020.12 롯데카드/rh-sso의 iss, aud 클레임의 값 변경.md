- rh-sso의 iss, aud 클레임의 값 변경
- access token의 개별 revoke
- access token의 개별 Lifespan 지정
   

iss, aud 클레임의 값 변경 및 access token의 revoke 방법 문의
 
마이데이터 대응 프로젝트를 진행중에 rh-sso 관련하여 도움을 요청드립니다.
 
1. 마이데이터 표준 API 규격에 JWT 클레임 중 iss, aud 의 값을 특정한 값으로 설정하도록 되어 있는데, rh-sso 이 발급하는 access token에는 iss에 realm의 URL이 들어가고, aud에는 "account" 라는 고정된 값이 들어가고 있어 두 claim을 원하는 값으로 변경할 방법이 있는지 문의드립니다.
2. 마이데이터 표준 API 규격에 발급된 access token을 revoke 할 수 있도록 되어 있는데, rh-sso는 client 단위로만 revoke 할 수 있는 것으로 보입니다. 개별 access token에 대해 revoke 할 방법이 있는지 문의드립니다.
3. 마이데이터 표준 API 규격에 access token 발급시 Lifespan을 지정할 수 있도록 되어 있는데, rh-sso 에서는 realm 단위로 설정하는 방법만 찾을 수 있었습니다. token 발급시마다 Lifespan을 동적으로 지정할 방법이 있는지 문의드립니다.