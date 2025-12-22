```
URL = '[http://confluence.apps.d-platform.doosan.com/admin/users/removeunsynceduser-confirm.action](http://confluence.apps.d-platform.doosan.com/admin/users/removeunsynceduser-confirm.action)';   
ATL_TOKEN = '2b4870e085175b6c892757a6464999e3894e766e';  
DELAY = 50;
```
 
```
USER_KEYS = [];  
cnt = 0;
```
   

```
function delete_unsynced_user(user_key) {  
    $.post(  
        URL,  
        {  
            'atl_token': ATL_TOKEN,  
            'userKey'  : user_key,  
            'confirm'  : 'Delete'  
        },  
        function(result) {  
            console.log('success', ++cnt, user_key);
```
 
```
            if (cnt == USER_KEYS.length) {  
                console.log('Finished. Refreshing Page...');  
                document.location.href = document.location.href;  
            }  
        }  
    );  
}
```
 
```
document.querySelectorAll('#browse-user-table a').forEach( (item, index) =\> {  
    if (!item.hasAttribute('data-username') && item.getAttribute('href').indexOf('=') \> 0) {  
        var href = item.getAttribute('href');  
        var user_key = href.split('=')[1];
```
 
```
        if (user_key.length == 32) {  
            USER_KEYS.push(user_key);  
        }  
    }  
});
```
 
```
console.log('total:', USER_KEYS.length);  
USER_KEYS.forEach( function(user_key, index) {  
    setTimeout( function() {  
        delete_unsynced_user(user_key);  
    }, index * DELAY);  
});
```