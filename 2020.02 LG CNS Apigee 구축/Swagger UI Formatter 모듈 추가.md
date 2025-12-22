```
### Swagger UI 라이브러리 추가  
$ mkdir -p /opt/d8-apigee-kickstart/web/libraries  
$ cd /opt/d8-apigee-kickstart/web/libraries  
$ wget [https:](https://github.com/swagger-api/swagger-ui/archive/v3.23.8.zip)//github.com/swagger-api/swagger-ui/archive/v3.23.8.zip  
$ unzip v3.23.8.zip  
$ mv swagger-ui-3.23.8 swagger-ui  
$ rm v3.23.8.zip  
   
   
### Swagger UI Formatter 모듈 설치  
$ composer require 'drupal/swagger_ui_formatter:^2.0' -vvv  
   
   
### Drupal 어드민 \> Extend \> 'Swagger UI Field Formatter' 모듈 활성화  
   
### Drupal 어드민 \> Structure \> API docs \> Manage display \> 'OpenAPI specification' 필드의 format 을 'Swagger UI' 로 변경
```
 ![image201999_201955png](Exported%20image%2020251106115832-0.png)