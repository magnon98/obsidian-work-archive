\> [!caution] This page contained a drawing which was not converted.   

```
$ curl [https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.8-stable/amp/amp.yml](https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.8-stable/amp/amp.yml) -o amp28.yaml
```
 
```
$ REGISTRY_DOMAIN=registry.example.com
```
 
```
$ cat amp28.yaml \  
    | sed 's/registry.redhat.io/'$DOMAIN'/' \  
    | sed 's/redis-32-rhel7:3.2/redis-5-rhel7:5/' \  
    | sed 's/rh-redis32/rh-redis5/' \> amp28-custom.yaml
```
 
```
$ oc new-project apim28
```
 
```
$ echo 'apiVersion: v1  
kind: Secret  
metadata:  
  name: threescale-registry-auth  
data:  
  .dockerconfigjson: eyJhdXRocyI6eyJyZWdpc3RyeS5yZWRoYXQuaW8iOnsiYXV0aCI6Ik1UQTVOelV6T1RaOFpXSmhlVHBsZVVwb1lrZGphVTlwU2xOVmVsVjRUV2xLT1M1bGVVcDZaRmRKYVU5cFNYZE9WRUV5V1cxU2FFNUVaM2haYWxFd1QwUkJlRmxVWnpOTk1sRjZXVmRTYlU1NlVUQk5SRnBxVFdsS09TNWlWQzFVWkhrNUxUZE5Tamh4TVdsWGRVcFVaV2Q0VlVGMldGTmtUazl4VW10MlpIVnVhazFUTTBONmFWTTRXVEp3YkdWRFRUWjZObmgwTTFOU1dqUkZTV1pGTWtaUlVHODBhSGsxUW1GdlZuaDNXa2xrU1Voa05XY3lRVlZRWVZaNE1IaHBjalIwVm5FeE1WazNaMjFPVDBsZlpGaHhjbWg1TlhsUllsWnpUWHB4YUZscVRIaEtPV1JQZVY5QmIzQnNNWFF5VTNwRlEyZFFiV3hCVDFNeVN6bGhjMnRqVEV3MVZUSkhSakZsYnpOM1ZVaDVjRXBKUTFSNE1qSkVXVmR6TW1wSVYwbFVUMHRGYkVGd2VuUnhWa2M1ZWtaYVFqa3pjSEpqY0VoVk1tVnNVMlJTWkY5bVQyNUNjbDlEY21wM05ISmxNRzVQVTJOS1RIWm9jMDlsTUdRMlNrUmxVbGMxWTFwTGJFZFdjRVl0TVVOTlNqTlFNRTVtYUhJeVFUQldibFUxV0hGWVpFRk1aMjlQYUdFME9GZFFVWGxGWTJwcWVYcE9XV2hQT1dKNVZIY3dXV2RDTUY5eWFuUjFPVVF6TVhSMlEwb3lOazlaVnpadE56WkRjemhTV2tWclFtVTVOa1l0VDFsQ1MxQTJTR3h2WDJoM2IxQkxlREJDVG10UVgzWTRkbHBNVldkWE5YbEpja2RyYzFKelltbDJVR3RwYTJjeVdXNHlMV1JoTVVSallsOTJXRWxXUlVOb1pXWkJWbXBSWm10U1RIaHhURWhKUW5ZMmNucERWVWRMU3pCaFRVbFJUV05xZW5odE1HcFZiRWwzYzJ4dlJrbHFabGcwYTFGbU4yWldlWFJET1hGdlkxRmhYMXBmYVVvM2FuWXdXVEJyTkRCcVkwVjRhekl5TWtoM1UwWlNiRXhwTWpoV1gzaHJXRWhDWWpSWllUaDVWV04xTUdoVlZGWTJha1l3ZGxoVVduWkdUVWxDU2xwdGRVbGlXVFJvZUZWRFkwOVRjR2QyYTA5Rk0wZEJhblZaVW5seGRFTnhRbmxhYkcxSFZETnNUVmRmV1VsV1NWOWZTRVZZV1RkcWFtczVUak14TTJacGExbFpPRWR2WkRabVVXOUNSMmRVU3psaGExZzBRVzlvUkdoSVVFbG9SRGt3WW1KeWJ6VmhOemhHY0VJMmIwMWhkMmxtVEVSNll3PT0ifX19  
type: kubernetes.io/dockerconfigjson' | oc create -f -
```
 
```
$ oc new-app -f amp28-custom.yaml \  
    -p WILDCARD_DOMAIN=apim28c.bliex.io \  
    -p ADMIN_USERNAME=admin \  
    -p ADMIN_PASSWORD=admin.! \  
    -p MASTER_USER=master \  
    -p MASTER_PASSWORD=master.!
```