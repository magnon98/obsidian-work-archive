\> [!caution] This page contained a drawing which was not converted.  

![Windows PowerShe11 Copyright C microsoft Corporati...](Exported%20image%2020251106125006-0.png)

```
const fetch = require('node-fetch')
```
 
```
const MS_ENDPOINT = '[http://192.168.100.38:8080](http://192.168.100.38:8080)'  
const ORG_NAME = 'validate'  
const USER_AUTH = 'canape@bliex.com:Qmfflrtm123$'  
const AUTH_HEADER = {  
    headers: {'Authorization': 'Basic ' + Buffer.from(USER_AUTH, "utf8").toString('base64')}  
}
```
   

```
async function retrieveApiList() {  
    const URL_API_LIST = MS_ENDPOINT + '/v1/organizations/' + ORG_NAME + '/apis'  
    const api_list = await fetch(URL_API_LIST, AUTH_HEADER).then(resp =\> resp.json())  
    // console.log('api_list:', api_list)  
    const result = await Promise.all(api_list.map(async api_name =\> {  
        const base_path = await retrieveBasePath(api_name)  
        return {  
            api_name,  
            base_path  
        }  
    }))  
    console.log('RESULT: \n' + JSON.stringify(result, null, 4))  
    return result  
}
```
    
```
async function retrieveBasePath(api_name) {  
    const URL_REVISION_LIST = MS_ENDPOINT + '/v1/organizations/' + ORG_NAME + '/apis/' + api_name + '/revisions'  
    const revision_list = await fetch(URL_REVISION_LIST, AUTH_HEADER).then(resp =\> resp.json())  
    // console.log('revision_list:', revision_list)  
    const max_revision = revision_list.sort().pop()  
    // console.log('max_revision', max_revision)  
    const URL_REVISION_INFO = URL_REVISION_LIST + '/' + max_revision  
    const revision_info = await fetch(URL_REVISION_INFO, AUTH_HEADER).then(resp =\> resp.json())  
    // console.log('revision_info:', revision_info)  
    return revision_info.basepaths.join(', ')  
}
```
    
```
retrieveApiList()
```