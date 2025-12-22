공통사항  
    접근제어 방식에 따라 적절한 credential 제공 필요  
    secure port 사용해야 외부에서 접근 가능(credential 필요)  
    어떤 방식을 사용하더라도 결국 api-server를 거치게 됨  
    yaml 또는 json을 인자로 활용 가능  
    master node 를 3개로 구성할 예정이므로 앞단에 reverse proxy를 구성해야 함. ( admin instance 내에?)
   

cli  
    java runtime에서 process를 호출하는 방식  
    kubectl을 builder에 설치 필요  
    master node에 접근할 수 있도록 설정 필요. (kubectl도 내부적으로는 api-server를 통해 제어)  
    초기 개발은 빠를 수 있으나 유지보수 어려움.
   

native rest api  
    api-server 컴포넌트가 제공하는 RESTful API  
    insecure port 는 127.0.0.1/32 or 0.0.0.0/0 만 설정 가능  
    보안 문제를 피하기 위해 외부에서 접속시 secure port를 사용  
    kubectl이 제공하는 대부분의 기능 사용 가능  
    yaml 대신 DTO 사용시 DTO --\> yaml 변환과정 필요.  
    **yaml을 통한 관리에 익숙한 경우 유리**
   

fabric8  
    api-server에서 제공하는 API 중 일부를 Java에서 사용하기 용이하도록 라이브러리화  
    아직 pods, replicationControllers, services 의 기본적인 기능에 대해서만 지원됨.  
    그외의 기능은 cli 혹은 native rest api 를 활용한 추가 개발 필요  
    secure access 가능한지 확인 필요. --\> 지원하는 것으로 보임.  
    **pod / service 관련 API만 필요한 경우 유리**
   

admin 과 builder에서 어느 선까지 필요할지에 따라 방향이 달라질 수 있음.  
- pod 과 service 에 대해서만 관리가 필요하다면 fabric8사용하는 것이 유리  
- log,  node 등의 관리용 API도 필요한 경우:  
- fabric8의 구조에 맞추어 필요한 API에 대응하는 코드 개발  
- fabric8이 제공하지 않는 API에 대응하는 코드만 개발하여 2-track으로 관리  
- native rest api를 직접 호출해서 사용.
 
dashboard용 등의 metric은 prometheus or heapster + prometheus를 통해 수집