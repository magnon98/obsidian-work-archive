```
$ cat gen_token.js  
const fs = require('fs');  
const jwt = require('jsonwebtoken')
```
 
```
const API_KEY='89c52dd6446b44b0a991d0926ee5bbb1'  
const CLIENT_SECRET='ebec3662-ee36-4ede-9d8d-e2dd56b14b1b'  
const IMS='ims-na1.adobelogin.com'  
const IMS_ORG='231F22CE527850C40A490D4D@AdobeOrg'  
const TECHNICAL_ACCOUNT_ID='0F332DFD5DD79CE20A495FA3@techacct.adobe.com'
```
 
```
const privateKey = fs.readFileSync('/path/to/launch_api.key')
```
 
```
/**  
 * exp: unix_timestamp  
 * iss: organization id  
 * sub: technical account id  
 * [https://ims-na1.adobelogin.com/s/ent_reactor_sdk](https://ims-na1.adobelogin.com/s/ent_reactor_sdk): ???  
 * aud: client URI ( [https://ims-na1.adobelogin.com/c/[API_KEY](https://ims-na1.adobelogin.com/c/[API_KEY)] )  
 */  
const payload = {  
  'exp': Math.floor(Date.now() / 1000) + 86400,  
  'iss': IMS_ORG,  
  'sub': TECHNICAL_ACCOUNT_ID,  
  'aud': '[https://ims-na1.adobelogin.com/c/](https://ims-na1.adobelogin.com/c/)' + API_KEY,  
  '[https://ims-na1.adobelogin.com/s/ent_reactor_sdk](https://ims-na1.adobelogin.com/s/ent_reactor_sdk)': true,  
}
```
 
```
const token = jwt.sign(payload, privateKey, { algorithm: 'RS256'})
```
 
```
console.log(token)
```
 
```
$ JWT_TOKEN=`node jwt.js`
```