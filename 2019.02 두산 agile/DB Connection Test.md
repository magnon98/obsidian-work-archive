```
Connection string  
jdbc:mysql://ddp-confluence-test.mysql.database.azure.com/atlassian?useSSL=true&autoReconnect=true&sessionVariables=tx_isolation='READ-COMMITTED'  
ID: atlassian@ddp-confluence-test  
PW: atl@123
```
    
```
keep alive ping  
    \<property name="hibernate.c3p0.preferredTestQuery"\>select 1\</property\>￼
```
 \> 출처: \<[https://confluence.atlassian.com/conf61/surviving-database-connection-closures-877188453.html](https://confluence.atlassian.com/conf61/surviving-database-connection-closures-877188453.html)\>