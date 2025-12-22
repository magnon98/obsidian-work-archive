# sysadmin인 경우 - Edge UI 에서 변경 불가
 
```
$ cat canape.xml  
\<User id="canape@bliex.com"\>  
  \<Password\>\<![CDATA[password_of_account]]\>\</Password\>  
  \<FirstName\>admin\</FirstName\>  
  \<LastName\>admin\</LastName\>  
  \<EmailId\>canape@bliex.com\</EmailId\>  
\</User\>
```
 
```
$ curl -v -H 'Authorization: Basic c2ticmFja2V0MUBzay5jb206UXdlcjEyMzQhQA==' \  
    -X POST [http://localhost:8080/v1/users/canape@bliex.com](http://localhost:8080/v1/users/canape@bliex.com) \  
    -H 'Content-Type: application/xml' \  
    -d @canape.xml
```
    
# sysadmin이 아닌 경우 - Edge UI 에서 변경 가능
    
# 또는 계정의 종류에 관계 없이

```
$ set +o history
```
 
```
$ apigee-service apigee-setup reset_user_password \  
    -a [sysadmin Email] -P [sysadmin PW] \  
    -u [user email] -p [user password]
```