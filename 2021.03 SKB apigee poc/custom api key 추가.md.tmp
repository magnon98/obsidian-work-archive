```
echo '\<CredentialRequest\>   
  \<Attributes/\>   
  \<ConsumerKey\>l7xx159a8ca72966400b886a93895ec9e2e3\</ConsumerKey\>   
  \<ConsumerSecret\>dummy-secret\</ConsumerSecret\>   
  \<ApiProducts\>   
    \<ApiProduct\>poc-product\</ApiProduct\>   
  \</ApiProducts\>   
  \<Scopes/\>   
\</CredentialRequest\>' \> app.xml
```
 
```
curl -v -u 'agwpoc@sk.com':'Agwpoc1!' \  
    -X POST '[http://10.10.214.211:8080/v1/o/validate/developers/agwpoc@sk.com/apps/poc-app/keys/create](http://10.10.214.211:8080/v1/o/validate/developers/agwpoc@sk.com/apps/poc-app/keys/create)' \  
    -H "Content-type: application/xml" \  
    -d @app.xml
```