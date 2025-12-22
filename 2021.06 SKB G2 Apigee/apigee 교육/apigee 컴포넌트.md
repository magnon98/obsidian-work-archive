```
apigee-zookeeper  
노드간 데이터 동기화 등을 자동으로 처리해주는 코디네이션 서비스 (분산형 스토리지?)  
Cassandra의 저장소로 사용됨
```
 
```
apigee-cassandra  
분산형 NoSQL 데이터베이스 - keyspace 내에 key-value 형태로 데이터를 저장  
Apigee의 메인 DB
```
 
```
apigee-openldap  
디렉토리 서비스  
계정 정보를 저장
```
 
```
edge-management-server  
Apigee 관리기능을 제공하는 Java application  
REST API 기반으로 기능을 제공
```
 
```
edge-ui  
Apigee의 웹콘솔을 제공하는 Java application  
Backend는 ms를 사용
```
 
```
edge-qpid-server  
qpidd를 관리하는 java application  
mp, ms 등은 qpidd 와 직접 연결되지 않고 edge-qpid-server를 통해 큐를 처리
```
 
```
apigee-qpidd  
AMQP 프로토콜을 사용하는 메시지 큐  
analytic data 적재시 MP - PostgreSQL 간 병목을 줄이기 위해 사용됨
```
 
```
edge-postgres-server  
postgresql 내의 analytic data를 관리하는 java application
```
 
```
apigee-postgresql  
alalytic data의 저장소
```