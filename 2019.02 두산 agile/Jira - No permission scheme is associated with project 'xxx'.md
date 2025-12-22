```
Adaptavist Scriptrunner or MyGroovy 플러그인을 사용해서 아래 코드 실행
```
   

```
import com.atlassian.jira.component.ComponentAccessor  
import com.atlassian.jira.permission.PermissionSchemeManager;  
import com.atlassian.jira.scheme.SchemeManager;  
import com.atlassian.jira.scheme.Scheme;  
   
def prList = ComponentAccessor.getProjectManager().getProjectByCurrentKey("PROJECT_KEY")  
PermissionSchemeManager permissionSchemeManager = ComponentAccessor.getPermissionSchemeManager();  
Scheme permissionScheme = permissionSchemeManager.getSchemeObject("PERMISSION_SCHEME");  
permissionSchemeManager.addSchemeToProject(prList, permissionScheme);
```
    \> 출처: \<[https://mraddon.blog/2018/11/12/no-permission-scheme-is-associated-with-project-xxxx-quickfix-for-jira-with-groovy-script/](https://mraddon.blog/2018/11/12/no-permission-scheme-is-associated-with-project-xxxx-quickfix-for-jira-with-groovy-script/)\>