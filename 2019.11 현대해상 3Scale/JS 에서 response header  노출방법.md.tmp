1. ```
    Policy 중 Header modification 으로 다음을 추가
    ```
    
    ```
    key: Access-Control-Expose-Headers
    ```
    
    ```
    value: 허용하고자 하는 키 값 (, 로 구분)
    ```
    

```
백엔드에서 response Header 에 Expose-Headers 헤더를 추가해도 가능.
```
 
```
Header Modification 사용시 네가지중 선택 가능
```

```
헤더가 있는 경우에만 값을 추가
```

```
헤더가 있으면 값을 변경
```

```
헤더가 없으면 생성, 있으면 값을 추가
```

```
헤더를 삭제
```
  
```
###### 테스트 코드
```
 
```
### server-side (node.js)  
const express = require('express')  
const app = express()
```
 
```
app.get('/', (request, response) =\> {  
    response.send('ok\n')  
})
```
   

```
app.post('/test', function (request, response) {  
  response.setHeader("Access-Control-Expose-Headers", "X-Header-Test");  
  response.setHeader('X-Header-Sample', 'sample')  
  response.setHeader('X-Header-Test', 'test')  
  response.send({test: 'ok'})  
})
```
 
```
app.listen(3333, function () {  
  console.log('Example app listening on port 3333!')  
})
```
      

```
### 브라우저에서 호출  
fetch('https://allow-header-test-3scale-apicast-staging.apim.bliex.io/test',{  
    'method': 'post',  
    'headers': {  
        'user-key': '6a3fe022795289f96bc3d5166a376ca8'  
    }  
}).then(response =\> {  
    for(let header of response.headers.entries()) {  
        console.log('headers:', header);  
    }
```
 
```
    return response.text()  
}).then(result =\> {  
    console.log(result)  
})
```