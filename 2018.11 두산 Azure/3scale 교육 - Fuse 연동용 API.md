```
backend api  
URL: [http://doosan-sample-api.apps.d-platform.doosan.com](http://doosan-sample-api.apps.d-platform.doosan.com)  
Path:  
[http://doosan-sample-api.apps.d-platform.doosan.com/swagger-ui.html](http://doosan-sample-api.apps.d-platform.doosan.com/swagger-ui.html)  
- GET /api/v1/doosan-sample-api/logs  
- GET /api/v1/doosan-sample-api/messages
```
   

```
(items 관련은 DB 가 없어서 사용 불가)  
- GET /api/v1/doosan-sample-api/items  
- POST /api/v1/doosan-sample-api/items  
- GET/PATCH/DELETE /api/v1/doosan-sample-api/items/{itemId}
```
 
```
secret token: Shared_secret_sent_from_proxy_to_API_backend_a0d7cceb279a5d1d
```
   

```
Fuse URL: [http://fuse-doosan-sample-api.apps.d-platform.doosan.com](http://fuse-doosan-sample-api.apps.d-platform.doosan.com)  
3Scale URL: [https://3scale-admin.apig.d-platform.doosan.com/apiconfig/services/3/integration/edit](https://3scale-admin.apig.d-platform.doosan.com/apiconfig/services/3/integration/edit)
```
            

```
curl -X GET "[http://doosan-sample-api.apps.d-platform.doosan.com/api/v1/doosan-sample-api/messages](http://doosan-sample-api.apps.d-platform.doosan.com/api/v1/doosan-sample-api/messages)" \  
 -H 'X-3scale-proxy-secret-token: Shared_secret_sent_from_proxy_to_API_backend_a0d7cceb279a5d1d' \  
 -H 'FUSE_REMOTE_USER: tester'
```