```
\<script type="text/javascript"\>  
const spec_list = [  
{% for app in current_account.applications %}  
    {% for spec in app.service.api_specs %}  
        {  
            'app_id': '{{ app.id }}',  
            'app_name': '{{ app.name }}',  
    
            'api_service_name': '{{ app.service.name }}',  
            'api_service_system_name': '{{ app.service.system_name }}',  
    
            'spec_name': '{{ spec.system_name }}',  
            'url': '{{ spec.url }}',  
        },  
    {% endfor %}  
{% endfor %}  
]
```
 
```
console.log(JSON.stringify(spec_list, null, 4))  
\</script\>
```