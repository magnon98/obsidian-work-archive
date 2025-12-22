```
Adobe Launch API
```
    
```
export API_KEY="89c52dd6446b44b0a991d0926ee5bbb1"  
export CLIENT_ID=$API_KEY  
export CLIENT_SECRET="ebec3662-ee36-4ede-9d8d-e2dd56b14b1b"  
export IMS="ims-na1.adobelogin.com"  
export IMS_ORG="231F22CE527850C40A490D4D@AdobeOrg"  
export TECHNICAL_ACCOUNT_ID="0F332DFD5DD79CE20A495FA3@techacct.adobe.com"
```
 
```
export JWT_TOKEN=`node ~/temp/gen_token`  
export ACCESS_TOKEN=`curl -sX POST "[https://ims-na1.adobelogin.com/ims/exchange/jwt/](https://ims-na1.adobelogin.com/ims/exchange/jwt/)" \  
   -H "Cache-Control: no-cache" \  
   -H "Content-Type: multipart/form-data" \  
   -F "client_id=$API_KEY" \  
   -F "client_secret=$CLIENT_SECRET" \  
   -F "jwt_token=$JWT_TOKEN" | jq -r .access_token`
```
    
# ### JWT Payload
 
```
/**  
 * exp: unix_timestamp  
 * iss: organization id  
 * sub: technical account id  
 * [https://ims-na1.adobelogin.com/s/ent_reactor_sdk](https://ims-na1.adobelogin.com/s/ent_reactor_sdk): ???  
 * aud: client URI ( [https://ims-na1.adobelogin.com/c/[cliend_id](https://ims-na1.adobelogin.com/c/[cliend_id)] )  
 */  
{  
    "exp": 1574498386,  
    "iss": "231F22CE527850C40A490D4D@AdobeOrg",  
    "sub": "0F332DFD5DD79CE20A495FA3@techacct.adobe.com",  
    "[https://ims-na1.adobelogin.com/s/ent_reactor_sdk](https://ims-na1.adobelogin.com/s/ent_reactor_sdk)": true,  
    "aud": "[https://ims-na1.adobelogin.com/c/89c52dd6446b44b0a991d0926ee5bbb1](https://ims-na1.adobelogin.com/c/89c52dd6446b44b0a991d0926ee5bbb1)"  
}
```
    
# ### get Access Token

```
curl -X POST "[https://ims-na1.adobelogin.com/ims/exchange/jwt/](https://ims-na1.adobelogin.com/ims/exchange/jwt/)" \  
  -H "Cache-Control: no-cache" \  
  -H "Content-Type: multipart/form-data" \  
  -F "client_id=89c52dd6446b44b0a991d0926ee5bbb1" \  
  -F "client_secret=ebec3662-ee36-4ede-9d8d-e2dd56b14b1b" \  
  -F "jwt_token=$JWT_TOKEN"   ```
 
# ### access token result

```
{  
  "token_type": "bearer",  
  "access_token": "eyJ4NXUiOiJpbXNfbmExLWtleS0xLmNlciIsImFsZyI6IlJTMjU2In0.eyJpZCI6IjE1NzQ0MTE2OTAwMzhfYTE2ZGY3ZTQtYTllYi00ZTIzLWFmZWEtYzE5Y2QyMmFlMmYzX3VlMSIsImNsaWVudF9pZCI6Ijg5YzUyZGQ2NDQ2YjQ0YjBhOTkxZDA5MjZlZTViYmIxIiwidXNlcl9pZCI6IjBGMzMyREZENURENzlDRTIwQTQ5NUZBM0B0ZWNoYWNjdC5hZG9iZS5jb20iLCJ0eXBlIjoiYWNjZXNzX3Rva2VuIiwiYXMiOiJpbXMtbmExIiwiZmciOiJUNlIyRjZUN0hMRjVMSFUyQ09RTEtLUUFIST09PT09PSIsIm1vaSI6IjE0OTYyNzkyIiwiYyI6InlnUm9oTUwvZzZxNC93OUp0Smdwdmc9PSIsImV4cGlyZXNfaW4iOiI4NjQwMDAwMCIsInNjb3BlIjoiYWRkaXRpb25hbF9pbmZvLmpvYl9mdW5jdGlvbixvcGVuaWQsQWRvYmVJRCxyZWFkX29yZ2FuaXphdGlvbnMsYWRkaXRpb25hbF9pbmZvLnJvbGVzLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTc0NDExNjkwMDM4In0.nZcOhL239tl_vcXr4-nZ5XBShVVxzkayMZpmOX9xwL8ZrQ3LQ-Z74askFmXpPtGh--wibXFKhJbvQLjuBdbR6yHaYikWwFNzBy_xqeiP5_rW9hKJxWbRUMHSiqvyWdUqKtF91GsIan5kSUFHFyw4-hjn4W06qd9Jwc5UakqPIMrarB0hd8ybsMgc-Zdk5cwA_PNs004pU8datav3cDP-EHVwSCTqBsUVvWeYnqwFJq3zf2GFmQy3ONPXAZuDtViZc4OLSzrAjAf_6Wog6jnHXMH4Z8iYHuux43Ov8Y6uAZ1mvRLDNvzyHbQJOBhVE22kozsAJQPd7_-c6d98idmE6w",  
  "expires_in": 86399993  
}
```
       
```
### companies - list  
curl -X GET [https://reactor.adobe.io/companies](https://reactor.adobe.io/companies) \  
  -H "Accept: application/vnd.api+json;revision=1" \  
  -H "Content-Type: application/vnd.api+json" \  
  -H "Authorization: Bearer $ACCESS_TOKEN" \  
  -H "X-Api-Key: $API_KEY" \  
  -H "X-Gw-Ims-Org-Id: $IMS_ORG"
```
   

```
export COMPANY_ID=COae164dc89349443cb5092e1fdc571f55
```
   

```
### properties - list  
curl -X GET [https://reactor.adobe.io/companies/$COMPANY_ID/properties](https://reactor.adobe.io/companies/$COMPANY_ID/properties) \  
  -H "Accept: application/vnd.api+json;revision=1" \  
  -H "Content-Type: application/vnd.api+json" \  
  -H "Authorization: Bearer $ACCESS_TOKEN" \  
  -H "X-Api-Key: $API_KEY" \  
  -H "X-Gw-Ims-Org-Id: $IMS_ORG"
```
   

```
export PROPERTY_ID=PRd9a17f61c79748daa0c83e4cf64bd579
```
    
```
### rule - list  
curl -X GET [https://reactor.adobe.io/properties/$PROPERTY_ID/rules](https://reactor.adobe.io/properties/$PROPERTY_ID/rules) \  
  -H "Accept: application/vnd.api+json;revision=1" \  
  -H "Content-Type: application/vnd.api+json" \  
  -H "Authorization: Bearer $ACCESS_TOKEN" \  
  -H "X-Api-Key: $API_KEY" \  
  -H "X-Gw-Ims-Org-Id: $IMS_ORG"
```
    
```
export RULE_ID=RLaff01bcc50044daa976714ab4c63fab5
```
 
```
### rule - fetch
```
 
```
curl -X GET [https://reactor.adobe.io/rules/$RULE_ID](https://reactor.adobe.io/rules/$RULE_ID) \  
  -H "Accept: application/vnd.api+json;revision=1" \  
  -H "Content-Type: application/vnd.api+json" \  
  -H "Authorization: Bearer $ACCESS_TOKEN" \  
  -H "X-Api-Key: $API_KEY" \  
  -H "X-Gw-Ims-Org-Id: $IMS_ORG"
```