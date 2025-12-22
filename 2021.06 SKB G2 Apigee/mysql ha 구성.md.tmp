```
### master
```
 
```
echo -e "\nserver-id=1\nlog-bin=mysql-bin" \>\> /etc/my.cnf  
systemctl restart mysqld  
mysql -u root -p
```
 
```
mysql\> create user 'apigee'@'10.10.214.128' identified by 'G2infra1!';  
mysql\> grant replication slave on *.* to 'apigee'@'10.10.214.128';  
mysql\> flush privileges;  
mysql\> flush tables with read lock;  
mysql\> quit
```
 
```
mysqldump -u root -p --all-databases --master-data=2 \> master_backup.sql  
scp master_backup.sql root@10.10.214.128:/root/
```
 
```
### slave
```
 
```
echo -e "\nserver-id=2\nlog-bin=mysql-bin" \>\> /etc/my.cnf  
systemctl restart mysqld
```
 
```
mysql -u root -p \< master_backup.sql  
mysql -u root -p
```
 
```
mysql\> change master to master_host='10.10.214.127',  
    -\> master_user='apigee',  
    -\> master_password='G2infra1!',  
    -\> master_port=3306,  
    -\> master_log_file='mysql-bin.000001',  
    -\> master_log_pos=323,  
    -\> GET_MASTER_PUBLIC_KEY=1;  
mysql\> start slave;  
mysql\> show slave status\G
```
    
```
### master  
mysql -u root -p  
mysql\> unlock tables;  
mysql\> use auth;  
mysql\> select * from auth_token_bak;  
mysql\> INSERT INTO auth_token_bak (stbId, token, mac_addr, temp_yn) VALUES ('stb_id', 'tokennn', 'macaddrrr', 'N');
```
    
```
### slave  
mysql\> select * from auth_token_bak;
```
   

```
### master  
mysql\> delete from auth_token_bak where stbId='stb_id';
```
   

```
### slave  
mysql\> select * from auth_token_bak;
```