```
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: apim28-01  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 10Gi  
  nfs:  
    path: /exports/apim28/apim28-01  
    server: etc.shinhan.local  
  persistentVolumeReclaimPolicy: Retain
```
 
```
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: apim28-02  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 10Gi  
  nfs:  
    path: /exports/apim28/apim28-02  
    server: etc.shinhan.local  
  persistentVolumeReclaimPolicy: Retain
```
 
```
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: apim28-03  
spec:  
  accessModes:  
  - ReadWriteOnce  
  capacity:  
    storage: 10Gi  
  nfs:  
    path: /exports/apim28/apim28-03  
    server: etc.shinhan.local  
  persistentVolumeReclaimPolicy: Retain
```
 
```
---  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: apim28-04  
spec:  
  accessModes:  
  - ReadWriteMany  
  capacity:  
    storage: 10Gi  
  nfs:  
    path: /exports/apim28/apim28-04  
    server: etc.shinhan.local  
  persistentVolumeReclaimPolicy: Retain
```
       
```
curl [https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.8-stable/amp/amp.yml](https://raw.githubusercontent.com/3scale/3scale-amp-openshift-templates/2.8-stable/amp/amp.yml) -o amp28.yml  
### edit memory limit  
### add volumeName to pvc ( spec.volumeName )
```
   

```
oc new-project apim28
```
 
```
oc describe project apim28
```
 
```
chown -R 1000350000:nfsnobody /exports/apim28
```
   

```
echo 'apiVersion: v1  
data:  
  .dockerconfigjson: eyJhdXRocyI6eyJyZWdpc3RyeS5yZWRoYXQuaW8iOnsidXNlcm5hbWUiOiIxMTM1MTc4MHxibGlleCIsInBhc3N3b3JkIjoiZXlKaGJHY2lPaUpTVXpVeE1pSjkuZXlKemRXSWlPaUprTW1ReE9XSXhOR0V3WWpjME1EUTVPR0ptTkdFME5XRm1ZV0U1TnpVelppSjkuaHFJQUl5ZjFscTV3RDR4SVJ5enpDX0RibldOSnhkM2N5VVZLcFhqZVJROGRCS2xOSzl4cUNEWVV3Y1g5STlaNm9pWDg1TkREYkY2ZjE2WlVqNDdyLW1Tcl9tTldrLTlaMDY5MVZkdlJrU3BCcEVuOVVnd2gyYXd3RnRjbmMtY3JWOXh1MDV4ZVdBUnZqM04zcXRVRG0yeXhGV0hTcHBKSTVSdDFtM2hjZDQ3eDM0V1hFLTI0ME5TcHFWbEwyVE9DcDZ1akdUTGdNV1JyY1d2MDhmOXE4X0FQVnBXZlZBU3pKbDVjUThwVWJIOG9RR3RQa2JMNVRqVmlhRWgtMGx6LTVubnBiTW4wNHNEZE5MLTNGRGVIbkFfUDRVb0JmTE5VVGRtOE9KSkhVUHlwMWtZUDYtd01BVE1VdWo0SW1DcGo3QnFhQnptQ05OOTNYR1NqenN3a1JaMV9EbnBfX3VWMjBTak9wcmxpaDRDOTROTzJWZ1lCY2hPa2VWZUVVWkNKckJkdFJScDlUb05UeHBkeTRpWXRpbFZUMy0zQ1B1MUhsU0x2UEJXNnZWRlhkRVVjb2lySnA5MW13RXAxLXVRdmlPWmxheEpDNFVpTE5NNVRrS2M0eHJxREpSWDdPeGVINGczVDl4bEJOODdNUVJ3UkxiYWNlNFBzSlNhaDN5Q3hpc3h4ZG11bDlDb1FYZFB6LUhxNF8zdE1BUGRQVHBwOTY4LWNhQkwwUDJ1YXFvOVd3Q3ZOLWJPNXMtMEtveFlDakFSM25haU9fdzIzMFRJNkxORklBd3JLTE5idlhjR1lUTXhBXy04VEEzd2Rob3NENEtvS3hvMnJER0UyMUVrSFE3R1lfMm43enlzd21nbXUwUWFkSTVtS243M3dKS2VVSGZTU0hUcVdxYm8iLCJhdXRoIjoiTVRFek5URTNPREI4WW14cFpYZzZaWGxLYUdKSFkybFBhVXBUVlhwVmVFMXBTamt1WlhsS2VtUlhTV2xQYVVwclRXMVJlRTlYU1hoT1IwVjNXV3BqTUUxRVVUVlBSMHB0VGtkRk1FNVhSbTFaVjBVMVRucFZlbHBwU2prdWFIRkpRVWw1WmpGc2NUVjNSRFI0U1ZKNWVucERYMFJpYmxkT1NuaGtNMk41VlZaTGNGaHFaVkpST0dSQ1MyeE9Temw0Y1VORVdWVjNZMWc1U1RsYU5tOXBXRGcxVGtSRVlrWTJaakUyV2xWcU5EZHlMVzFUY2w5dFRsZHJMVGxhTURZNU1WWmtkbEpyVTNCQ2NFVnVPVlZuZDJneVlYZDNSblJqYm1NdFkzSldPWGgxTURWNFpWZEJVblpxTTA0emNYUlZSRzB5ZVhoR1YwaFRjSEJLU1RWU2RERnRNMmhqWkRRM2VETTBWMWhGTFRJME1FNVRjSEZXYkV3eVZFOURjRFoxYWtkVVRHZE5WMUp5WTFkMk1EaG1PWEU0WDBGUVZuQlhabFpCVTNwS2JEVmpVVGh3VldKSU9HOVJSM1JRYTJKTU5WUnFWbWxoUldndE1HeDZMVFZ1Ym5CaVRXNHdOSE5FWkU1TUxUTkdSR1ZJYmtGZlVEUlZiMEptVEU1VlZHUnRPRTlLU2toVlVIbHdNV3RaVURZdGQwMUJWRTFWZFdvMFNXMURjR28zUW5GaFFucHRRMDVPT1ROWVIxTnFlbk4zYTFKYU1WOUVibkJmWDNWV01qQlRhazl3Y214cGFEUkRPVFJPVHpKV1oxbENZMmhQYTJWV1pVVlZXa05LY2tKa2RGSlNjRGxVYjA1VWVIQmtlVFJwV1hScGJGWlVNeTB6UTFCMU1VaHNVMHgyVUVKWE5uWldSbGhrUlZWamIybHlTbkE1TVcxM1JYQXhMWFZSZG1sUFdteGhlRXBETkZWcFRFNU5OVlJyUzJNMGVISnhSRXBTV0RkUGVHVklOR2N6VkRsNGJFSk9PRGROVVZKM1VreGlZV05sTkZCelNsTmhhRE41UTNocGMzaDRaRzExYkRsRGIxRllaRkI2TFVoeE5GOHpkRTFCVUdSUVZIQndPVFk0TFdOaFFrd3dVREoxWVhGdk9WZDNRM1pPTFdKUE5YTXRNRXR2ZUZsRGFrRlNNMjVoYVU5ZmR6SXpNRlJKTmt4T1JrbEJkM0pMVEU1aWRsaGpSMWxVVFhoQlh5MDRWRUV6ZDJSb2IzTkVORXR2UzNodk1uSkVSMFV5TVVWclNGRTNSMWxmTW00M2VubHpkMjFuYlhVd1VXRmtTVFZ0UzI0M00zZEtTMlZWU0daVFUwaFVjVmR4WW04PSJ9fX0=  
kind: Secret  
metadata:  
  creationTimestamp: null  
  name: threescale-registry-auth  
type: kubernetes.io/dockerconfigjson' | oc create -f -
```
    
```
oc new-app \  
    -f amp28.yml \  
    -p WILDCARD_DOMAIN=amp.shinhan.local \  
    -p ADMIN_PASSWORD='admin.!' \  
    -p MASTER_PASSWORD='master.!'
```