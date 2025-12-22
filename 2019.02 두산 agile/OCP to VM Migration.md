```
2019.12.03 ~ 2019.12.06
```
   

```
### 접속정보
```
 
```
Host ddp-jira-01  
 Hostname 52.141.6.186  
 User jiradbadmin  
 IdentityFile ~/.ssh/ssh-keys/ddp-atlassian-rsa
```
 
```
Host ddp-confl-01  
 Hostname 52.141.39.230  
 User jiradbadmin  
 IdentityFile ~/.ssh/ssh-keys/ddp-atlassian-rsa
```
 
```
Host ddp-crowd-01  
 Hostname 52.141.6.40  
 User jiradbadmin  
 IdentityFile ~/.ssh/ssh-keys/ddp-atlassian-rsa
```
    
```
jiradbadmin // MlYA4rAt9He1
```
    
```
### OS 업데이트  
yum update
```
   

```
### mysql 설치  
yum install rh-mysql57
```
   

```
### jira / confluence 권장 튜닝 값 적용  
vi /etc/opt/rh/rh-mysql57/my.cnf  
[mysqld]  
binlog_format=row  
character_set_server=utf8mb4  
collation_server=utf8mb4_bin  
default_storage_engine=INNODB  
innodb_default_row_format=DYNAMIC  
innodb_file_format=Barracuda  
innodb_large_prefix=ON  
innodb_log_file_size=2GB  
max_allowed_packet=256M  
sql_mode=NO_AUTO_VALUE_ON_ZERO
```
   

```
### 서비스 재시작 및 자동실행 설정  
systemctl restart rh-mysql57-mysqld  
systemctl enable rh-mysql57-mysqld
```
   

```
### root password 변경  
$ mysql -u root -p  
mysql\> ALTER USER root@'localhost' IDENTIFIED BY 'Passw0rd!123';  
mysql\> flush privileges;
```
   

```
### jira / confluence / crowd 용 DB 계정 생성  
mysql\> CREATE DATABASE jira CHARACTER SET utf8 COLLATE utf8_bin;  
mysql\> create user 'jira'@'%' identified by '123qwer@';  
mysql\> GRANT ALL PRIVILEGES ON jira.* TO 'jira'@'%' IDENTIFIED BY '123qwer@';  
mysql\> flush privileges;
```
   

```
mysql\> CREATE DATABASE confluence CHARACTER SET utf8 COLLATE utf8_bin;  
mysql\> create user 'confluence'@'%' identified by '123qwer@';  
mysql\> GRANT ALL PRIVILEGES ON confluence.* TO 'confluence'@'%' IDENTIFIED BY '123qwer@';  
mysql\> flush privileges;
```
   

```
mysql\> CREATE DATABASE crowd CHARACTER SET utf8 COLLATE utf8_bin;  
mysql\> create user 'crowd'@'%' identified by '123qwer@';  
mysql\> GRANT ALL PRIVILEGES ON crowd.* TO 'crowd'@'%' IDENTIFIED BY '123qwer@';  
mysql\> flush privileges;
```
       
```
### 데이터용 디스크 추가  
# fdisk /dev/sdc  
# pvcreate /dev/sdc1  
# vgcreate storage /dev/sdc1  
# lvcreate -n atlassian-data -l 100%Free storage  
# mkfs.xfs /dev/mapper/storage-atlassian--data  
# mkdir /var/atlassian  
# mount /dev/mapper/storage-atlassian--data /var/atlassian  
# vi /etc/fstab  
/dev/mapper/storage-atlassian--data       /var/atlassian          xfs     defaults        0 0
```
       
```
### Jira 설치  
# wget [https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-7.13.1-x64.bin](https://product-downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-7.13.1-x64.bin)  
# chmod a+x atlassian-jira-software-7.13.1-x64.bin  
# ./atlassian-jira-software-7.13.1-x64.bin
```
    
```
### confluence 설치
```
      

```
### crowd 설치
```