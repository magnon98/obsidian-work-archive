```
10.95.30.101:30020
```
   

```
$ echo 'FROM docker-registry.default.svc:5000/openshift/java  
copy ./nice-tran-gateway-0.0.1-SNAPSHOT.jar /  
CMD java -Dnice.tcp.host=$TARGET_HOST -Dnice.tcp.port=$TARGET_PORT -jar /nice-tran-gateway-0.0.1-SNAPSHOT.jar' \> Dockerfile
```
    
```
$ docker build . -t docker-registry.default.svc:5000/test/fuse-gateway
```
    
```
$ oc new-project fuse-gateway  
$ oc run fuse-gateway --image=docker-registry.default.svc:5000/test/fuse-gateway  
$ oc set env dc/gateway TARGET_HOST=192.168.100.100 TARGET_PORT=5000
```
      

```
$ curl -X POST '[http://](http://localhost:8080/api/tran/73020)localhost:8080/api/tran/73020' \  
-H 'Content-Type: application/json' \  
-d '{  
"tran_grp_cd": "NICEIF",     
"kind_cd": "0200",  
"tx_cd": "73020",  
"snr_flag": "B",  
"term_gb": "503",  
"rsp_cd": "",      
"cert_id": "WS01",       
"inst_mng_no": "",            
"inst_send_time": "00000000000000",  
"nice_mng_no": "0000000000",  
"nice_send_time": "00000000000000",  
"ind_gb": "2",  
"reg_no": "1168115020",     
"inq_rsn_cd": "90",  
"name": "NICE평가정보",  
"etc_gb": "",  
"etc_reg_no": ""  
}'
```