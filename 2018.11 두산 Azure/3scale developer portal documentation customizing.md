```
\<h1\>Documentation\</h1\>  
\<div id="no_specs" style="display:none;"\>  
\<ul\>  
{% for app in current_account.applications %}  
    {% if {{provider.api_specs[app.service.system_name]["url"]}}? %}  
      	\<li\>\<a href="/docs?spec={{app.service.system_name}}"\>{{app.service.name}}\</a\>\</li\>  
    {% endif %}  
{% endfor %}  
\</ul\>  
\</div\>
```
   

```
{% cdn_asset /swagger-ui/2.2.10/swagger-ui.js %}  
{% cdn_asset /swagger-ui/2.2.10/swagger-ui.css %}
```
 
```
{% include 'shared/swagger_ui' %}
```
 
```
\<script type="text/javascript"\>  
$(function () {  
var create_all_specs_if_spec_not_specified = false;
```
 
```
  	{% comment %}  
{% for app in current_account.applications %}  
console.log('app.name: {{app.name}}');  
console.log('app.id: {{app.id}}');  
console.log('app.application_id: {{app.application_id}}');  
console.log('app.service.system_name: {{app.service.system_name}}');  
console.log('app.service.url: {{app.service.url}}');  
{% endfor %}  
  	{% endcomment %}
```
 
```
// retrieve list of all swagger specs  
    // api_spec's system name must match service's system_name exactly  
    var specs = {  
{% for app in current_account.applications %}  
'{{app.service.system_name}}': '{{provider.api_specs[app.service.system_name]["url"]}}',  
{% endfor %}  
    };  
console.log('specs:', specs);  
console.log('spec keys:', Object.keys(specs));
```
 
```
var swagger_section = document.querySelector('.swagger-section');
```
 
```
// create new swagger ui  
function create_swagger_ui(spec_names) {  
console.log('create_swagger_ui - spec_names:', spec_names);
```
 
```
for (var i = 0; i \< spec_names.length; i++) {  
var spec_name = spec_names[i];
```
 
```
// create div container for swagger ui  
    var container = document.createElement('div');  
    container.setAttribute('id', 'swagger-ui-container-' + spec_name);  
    container.classList.add('swagger-ui-wrap');  
    swagger_section.appendChild(container);
```
 
```
// add some spaces between UIs  
    var spacer = document.createElement('div');  
    spacer.style.height = '50px';  
    swagger_section.appendChild(spacer);
```
 
```
// create swagger ui & load spec  
    new SwaggerUi({  
        url: parent.document.location.origin + specs[spec_name],  
        dom_id: container.id,  
        //supportedSubmitMethods: ['get', 'post', 'put', 'delete', 'patch'],  
        // apisSorter: 'alpha',  
        // operationsSorter: 'method', // can also be 'alpha' or a function  
        onComplete: function(swaggerApi, swaggerUi) {  
            $('#' + container.id + ' pre code').each(function(i, e) {hljs.highlightBlock(e)});  
        },  
        docExpansion: 'list',  
        transport: function (httpClient, obj) {  
            console.log("[swagger-ui]\>\>\> custom transport. httpClient -", httpClient);  
            console.log("[swagger-ui]\>\>\> custom transport. obj -", obj);  
                    // return ApiDocsProxy.execute(httpClient, obj);  
                    return httpClient.execute(obj);  
        }  
    }).load();  
        }  
}
```
   

```
// get swagger spec name from url  
function get_specs_from_parent_window() {  
          // if (typeof parent != 'undefined' && parent !== window) {  
var params = new URLSearchParams(parent.document.location.search);  
if (params.has('spec')) {  
 return params.getAll('spec');  
}  
// }  
if (create_all_specs_if_spec_not_specified) {  
return Object.keys(specs);  
        }
```
 
```
return [];  
}
```
 
```
var target_specs = get_specs_from_parent_window();  
if (target_specs.length == 0) {  
document.querySelector('#no_specs').style.display = 'block';  
}  
else {  
create_swagger_ui(target_specs);  
}  
});
```
   

```
// Polyfill for IE11  
(function (w) {  
    w.URLSearchParams = w.URLSearchParams || function (searchString) {  
        var self = this;  
        self.searchString = searchString.substr(1);  
      
```
 
```
self.getAll = function (name) {  
var pairs = self.searchString.split('&');  
       		console.log('URLSearchParams polyfill - pairs:', pairs);
```
 
```
var ret = [];  
for (var i = 0; i \< pairs.length; i++) {  
var pair = pairs[i].split('=');  
if (pair.length != 2) {  
continue;  
}  
if (pair[0] == name && ret.indexOf(pair[1]) == -1) {  
ret.push(pair[1]);  
}  
}  
return ret;  
        };  
          
        self.get = function (name) {  
            return self.getAll(name).length \> 0 ? self.getAll(name)[0] : null;  
        };
```
 
```
        self.has = function (name) {  
            return self.getAll(name).length \> 0;  
        };
```
 
```
    }  
})(window)  
\</script\>
```