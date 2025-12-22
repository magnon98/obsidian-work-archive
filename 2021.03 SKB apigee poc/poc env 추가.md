```
export ADMIN_EMAIL=agwpoc@sk.com  
export ADMIN_PASSWORD='Agwpoc1!'  
export EDGE_SERVER=10.10.214.211
```
    
```
apigee-adminapi.sh orgs envs add -o validate -e poc
```
 
```
## uuid of MPs  
apigee-adminapi.sh orgs envs servers list -o validate -e test
```
 
```
apigee-adminapi.sh orgs envs servers add -o validate -e poc -u ********-4df1-48c8-8c07-************  
apigee-adminapi.sh orgs envs servers add -o validate -e poc -u ********-3c9a-4d91-9ccf-************
```
 
```
apigee-adminapi.sh orgs envs virtual_hosts add -o validate -e poc -v default -p 8888 -a agw-poc.sk-iptv.com
```
 
```
apigee-adminapi.sh orgs envs analytics scopes add -o validate -e poc -g axgroup-001
```