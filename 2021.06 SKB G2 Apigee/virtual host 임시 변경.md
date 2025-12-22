```
curl -X PUT [http://10.10.214.126:8080/v1/o/media/e/stg/virtualhosts/default](http://10.10.214.126:8080/v1/o/media/e/stg/virtualhosts/default) \  
    -u 'canape@bliex.com' \  
    -H 'Content-Type: application/xml' \  
    -d '\<VirtualHost name="default"\>  
   \<HostAliases\>  
      \<HostAlias\>agw-stg.sk-iptv.com\</HostAlias\>  
   \</HostAliases\>  
   \<Interfaces\>\</Interfaces\>  
   \<Port\>80\</Port\>  
\</VirtualHost\>'
```
      

```
curl -X PUT [http://10.10.214.126:8080/v1/o/media/e/stg/virtualhosts/http8085](http://10.10.214.126:8080/v1/o/media/e/stg/virtualhosts/http8085) \  
    -u 'canape@bliex.com' \  
    -H 'Content-Type: application/xml' \  
    -d '\<VirtualHost name="http8085"\>  
   \<HostAliases\>  
      \<HostAlias\>agw-stg.sk-iptv.com\</HostAlias\>  
   \</HostAliases\>  
   \<Interfaces\>\</Interfaces\>  
   \<Port\>8085\</Port\>  
\</VirtualHost\>'
```
      

```
curl -X PUT [http://10.10.214.126:8080/v1/o/media/e/stg/virtualhosts/http8090](http://10.10.214.126:8080/v1/o/media/e/stg/virtualhosts/http8090) \  
    -u 'canape@bliex.com' \  
    -H 'Content-Type: application/xml' \  
    -d '\<VirtualHost name="http8090"\>  
   \<HostAliases\>  
      \<HostAlias\>agw-stg.sk-iptv.com\</HostAlias\>  
   \</HostAliases\>  
   \<Interfaces\>\</Interfaces\>  
   \<Port\>8090\</Port\>  
\</VirtualHost\>'
```