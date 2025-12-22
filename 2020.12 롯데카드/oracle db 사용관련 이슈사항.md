```
1. OCP 4.x 에서는 Operator를 이용한 설치만 지원  
[https://access.redhat.com/documentation/en-us/red_hat_3scale_api_management/2.9/html-single/installing_3scale/index#deploying-threescale-on-openshift-using-template](https://access.redhat.com/documentation/en-us/red_hat_3scale_api_management/2.9/html-single/installing_3scale/index#deploying-threescale-on-openshift-using-template)
```
 ![23 Deploying 3scale on OpenShift using a template ...](Exported%20image%2020251106120037-0.png)  

```
실제로는 template 기반으로 설치 가능하지만, 레드햇의 지원이 제한될 수 있는지 확인 필요
```
       
```
2. Oracle DB는 OCP 3.11 에서만 지원하는 것으로 표기됨  
[https://access.redhat.com/articles/2798521](https://access.redhat.com/articles/2798521)
```
 ![3scale API Management 29 has been tested and its s...](Exported%20image%2020251106120038-1.png)  

```
template 설치가 필요하기 때문인 것으로 보임.   
operator 사용하여 설치하는 경우 system-app 등 mysql에 접근해야 하는 POD의 dc에  
수동으로 env 설정을 하는 경우, operator 때문에 env 설정이 유지되지 않음  
operator 에서 설정 변경을 지원해 주어야 함.
```
   

```
3. apimanager-reference 에서는 ORACLE_SYSTEM_PASSWORD 옵션이 제공되고 있음.  
apimanager yaml 에서 system.image 로 이미지도 변경 가능  
operator 이용한 oracle 설치도 불가능하진 않아 보임.
```
 
```
[https://github.com/3scale/3scale-operator/blob/master/doc/apimanager-reference.md#systemspec](https://github.com/3scale/3scale-operator/blob/master/doc/apimanager-reference.md#systemspec)
```