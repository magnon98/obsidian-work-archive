edge home  
- docker api를 통해 컨테이너 정보 추출  
- chromium 커스텀 빌드  
- minimal base image 선택  
- beluga agent 와 웹서버 분리  
- 도커 컨테이너 스스로 재시작할 방법  
- 디자인 입히기
       
docker run -d -p 9090:9090 -v /var/run/docker.sock:/var/run/docker.sock agent/armhf/beluga-agent
    
curl --unix-socket /var/run/docker.sock [http://localhost/containers/json](http://localhost/containers/json)
 
curl --unix-socket /var/run/docker.sock [http://localhost/networks](http://localhost/networks)
 
curl -XPOST --unix-socket /var/run/docker.sock [http://localhost/containers/$HOSTNAME/restart](http://localhost/containers/$HOSTNAME/restart)
 
curl --unix-socket /var/run/docker.sock [http://localhost/nodes](http://localhost/nodes)
 
curl --unix-socket /var/run/docker.sock [http://localhost/nodes](http://localhost/nodes) | jq -r .[0].Status.Addr
   

curl --unix-socket /var/run/docker.sock [http://localhost/containers/$HOSTNAME/json](http://localhost/containers/$HOSTNAME/json) | jq .  
curl --unix-socket /var/run/docker.sock [http://localhost/containers/$HOSTNAME/json](http://localhost/containers/$HOSTNAME/json) | jq .Config.Env