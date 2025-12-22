```
export API_KEY="VRZKC-5BSTD-4EWS3-R2J59-B8GYB"  
export API_TOKEN="c9cb3c65-91b2-4747-a8a9-9a0f79c2f563"
```
 
```
curl -H "Authentication: " \  
  [https://mpulse.soasta.com/concerto/mpulse/api/v2](https://mpulse.soasta.com/concerto/mpulse/api/v2)
```
 
```
### get security token  
SECURITY_TOKEN=`curl -X PUT "[https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Tokens](https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Tokens)" \  
    -H "Content-type: application/json" \  
    --data-binary '{"apiToken":"c9cb3c65-91b2-4747-a8a9-9a0f79c2f563"}' | jq -r .token`
```
   

```
{"token":"84592e64-a6238f-4378-90a8-9b23a1270a31"}
```
   

```
export SECURITY_TOKEN="826bd5f0-a0438e-4782-a51b-64ac1debd9ef"
```
   

```
### get user list  
curl "[https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Objects/user](https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Objects/user)" \  
    --header "X-Auth-Token: $SECURITY_TOKEN"
```
 
```
### get user list with attribute filter  
curl "[https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Objects/user?userAdministrator=true](https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Objects/user?userAdministrator=true)" \  
    --header "X-Auth-Token: $SECURITY_TOKEN"
```
 
```
### get user with id  
curl "[https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Objects/user/{id}](https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Objects/user/{id})" \  
    --header "X-Auth-Token: $SECURITY_TOKEN"
```
 
```
curl -vvv "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/summary?date=2019-10-31&format=json](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/summary?date=2019-10-31&format=json)" \  
    --header "Authentication: $SECURITY_TOKEN"
```
       
```
curl -vvv -X DELETE "[https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Tokens/{{SECURITY_TOKEN}}](https://mpulse.soasta.com/concerto/services/rest/RepositoryService/v1/Tokens/{{SECURITY_TOKEN}})"
```
   

```
summary  
histogram  
sessions-per-page-load-time  
metric-per-page-load-time  
by-minute  
geography  
page-groups  
browsers  
bandwidth  
ab-tests  
timers-metrics (for Navigation Timing, Custom Timers, and Custom Metrics)  
metrics-by-dimension  
dimension-values
```
       
```
curl -vvv -H "Authentication: $SECURITY_TOKEN" \  
    "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/metrics-by-dimension?dimension=device_type&date=2019-10-31&series-format=json&format=json](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/metrics-by-dimension?dimension=device_type&date=2019-10-31&series-format=json&format=json)"
```
   

```
curl -H "Authentication: $SECURITY_TOKEN" \  
  "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-over-time?dimension=operating_system&date=2019-10-31&series-format=json&format=json](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-over-time?dimension=operating_system&date=2019-10-31&series-format=json&format=json)"
```
 
```
curl -H "Authentication: $SECURITY_TOKEN" \  
  "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-over-time?dimension=operating_system&date-comparator=Between&date-start=2019-11-07T05:00:00Z&date-end=2019-11-07T06:00:00Z&series-format=json&format=json&timer=TimeToInteractive](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-over-time?dimension=operating_system&date-comparator=Between&date-start=2019-11-07T05:00:00Z&date-end=2019-11-07T06:00:00Z&series-format=json&format=json&timer=TimeToInteractive)"
```
   

```
curl -H "Authentication: $SECURITY_TOKEN" \  
  "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-over-time?dimension=device_type&date-comparator=Between&date-start=2019-11-07T05:00:00Z&date-end=2019-11-07T06:00:00Z&series-format=json&format=json&timer=TimeToInteractive](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-over-time?dimension=device_type&date-comparator=Between&date-start=2019-11-07T05:00:00Z&date-end=2019-11-07T06:00:00Z&series-format=json&format=json&timer=TimeToInteractive)"
```
   

```
curl -H "Authentication:  $SECURITY_TOKEN" \  
  "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-values?date=2019-10-31&dimension=beacon-type&beacon-type=page%20view&series-format=json&format=json](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-values?date=2019-10-31&dimension=beacon-type&beacon-type=page%20view&series-format=json&format=json)"
```
    
```
curl -vvv -H "Authentication: $SECURITY_TOKEN" \  
    "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/summary?date=2019-10-31&format=json](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/summary?date=2019-10-31&format=json)"
```
    
```
curl -vvv -H "Authentication: $SECURITY_TOKEN" \  
    "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/timers-metrics?timer=PageLoad&series-format=json&format=json](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/timers-metrics?timer=PageLoad&series-format=json&format=json)"
```
             
```
### 국가 목록 조회 (samsung.com의 국가 목록이 아님. akamai의 전체 236개 국가 목록)  
curl -vvv -H "Authentication: $SECURITY_TOKEN" \  
    "[https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-values?format=json&dimension=country&series-format=json](https://mpulse.soasta.com/concerto/mpulse/api/v2/$API_KEY/dimension-values?format=json&dimension=country&series-format=json)"
```