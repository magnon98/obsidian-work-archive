```
### create zip archive  
cd ./G1  
zip -r ../G1.zip ./apiproxy
```
 
```
cd ../G2-JWT  
zip -r ../G2-JWT.zip ./apiproxy
```
 
```
cd ../G2-VM  
zip -r ../G2-VM.zip ./apiproxy
```
 
```
cd ../MSA  
zip -r ../MSA.zip ./apiproxy
```
 
```
cd ../NextPaaS  
zip -r ../NextPaaS.zip ./apiproxy
```
 
```
cd ../Rate-Test  
zip -r ../Rate-Test.zip ./apiproxy
```
    
```
### api_list  
apigee-adminapi.sh orgs apis list -o validate | jq -r .[] \> ./api_list_to_keep.txt
```
   

```
apigee-adminapi.sh orgs apis list -o validate | jq -r .[] \  
    | egrep -v "$(echo -n '^'; cat ./api_list_to_keep.txt \  
    | tr '\n' '|' \  
    | sed 's/|/$|^/g' \  
    | head -c -2)" \> api_list_to_remove.txt
```
    
```
### undeploy
```
 
```
CNT=1  
time for API_NAME in $(cat api_list_to_remove.txt); do  
    apigee-adminapi.sh orgs apis undeploy -o validate -e test -a $API_NAME -r 1 -Y \> /dev/null  
    echo $CNT - undeploying $API_NAME...  
    CNT=$(($CNT + 1))  
done
```
   

```
### remove  
CNT=1  
time for API_NAME in $(cat api_list_to_remove.txt); do  
    apigee-adminapi.sh orgs apis delete -o validate -a $API_NAME -Y \> /dev/null  
    echo $CNT - deleting $API_NAME...  
    CNT=$(($CNT + 1))  
done
```