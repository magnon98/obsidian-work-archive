```
nginx conf  
upstream upstream_grafana {  
    server 50.1.111.186:3000;  
}  
server {  
...  
    location /grafana {  
        proxy_pass        [http://upstream_grafana](http://upstream_grafana);  
        rewrite ^/grafana/(.*)$ /$1 break;  
        proxy_set_header  Host $host;  
    }  
...  
}
```
    
```
$ sudo vi /usr/share/grafana/conf/defaults.ini  
# root_url = %(protocol)s://%(domain)s:%(http_port)s/  
root_url = %(protocol)s://%(domain)s:%(http_port)s/grafana  
[auth.anonymous]  
# enabled = false  
enabled = true
```
   

```
/usr/share/grafana/public/dashboards/scripted*.js  
[http://50.1.111.185/grafana/dashboard/script/scripted_*.js](http://50.1.111.185/grafana/dashboard/script/scripted_*.js)  
anonymous 허용하면 모두 접근되어 버림  
     dashboard.editable = false;  
     dashboard.hideControl = true;  
     로 추가 설정  
사용자별 필터링은 container_name에 대해 exact match 사용  
target을 여러개 지정해서 expression을 여러 개 사용하면 하나의 차트에 여러 개의 data 보여줄 수 있음.  
grafana의 헤더 처리 문제.  
     - div.navbar 생성 감지해서 제거하는 방법  
     -
```