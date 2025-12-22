OLD_PG1='4b1705e7-e391-4e02-bde4-a695dc68730f'  
OLD_PG2='7795e101-7174-48df-ae88-eb3e967db5ae'  
NEW_PG1='5d211797-960c-4bf3-b100-94a7a83d16f1'  
NEW_PG2='513c19a3-0fcc-4f53-8605-c005e7d5a347'
 
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X DELETE -H 'Accept: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/datastores/](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/datastores/$OLD_PG1,$OLD_PG2)$OLD_PG1,$OLD_PG2"  
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X DELETE -H 'Accept: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=$OLD_PG1,$OLD_PG2&type=postgres-server)$OLD_PG1,$OLD_PG2&type=postgres-server"
 
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X POST -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=$NEW_PG1,$NEW_PG2&type=postgres-server&force=true)$NEW_PG1,$NEW_PG2&type=postgres-server&force=true"  
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X POST -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/datastores?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/datastores?uuid=$NEW_PG1,$NEW_PG2)$NEW_PG1,$NEW_PG2"
      

OLD_QS1='d2057f87-6d17-4528-82eb-00f85b3c0da4'  
OLD_QS2='dd0eb21d-e08f-47e8-9f3c-29a1eb20db74'  
NEW_QS1='8264706e-5e75-4fb5-9ce7-01ff0a459650'z`  
NEW_QS2='fb6c34b4-25ed-41de-9123-2cb2dc06a5fb'
 
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X DELETE -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers/](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers/$OLD_QS1)$OLD_QS1"  
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X DELETE -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=$OLD_QS1&type=qpid-server)$OLD_QS1&type=qpid-server"
 
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X DELETE -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers/](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers/$OLD_QS2)$OLD_QS2"  
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X DELETE -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=$OLD_QS2&type=qpid-server)$OLD_QS2&type=qpid-server"
   

curl -v -u magnon@bliex.com:Qmfflrtm123$ -X POST -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers?uuid=$NEW_QS1)$NEW_QS1"  
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X POST -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=$NEW_QS1&type=qpid-server&force=true)$NEW_QS1&type=qpid-server&force=true"
 
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X POST -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/consumer-groups/consumer-group-001/consumers?uuid=$NEW_QS2)$NEW_QS2"  
curl -v -u magnon@bliex.com:Qmfflrtm123$ -X POST -H 'Content-Type: application/json' "[http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=](http://192.168.100.90:8080/v1/analytics/groups/ax/axgroup-001/servers?uuid=$NEW_QS2&type=qpid-server&force=true)$NEW_QS2&type=qpid-server&force=true"