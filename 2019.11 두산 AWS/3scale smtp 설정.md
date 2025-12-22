```
kind: ConfigMap  
apiVersion: v1  
metadata:  
  name: smtp  
  namespace: apim27  
  selfLink: /api/v1/namespaces/apim27/configmaps/smtp  
  uid: 41ea476a-3b6d-44bc-8829-d212240667ce  
  resourceVersion: '16220169'  
  creationTimestamp: '2020-03-06T04:01:06Z'  
  labels:  
    app: 3scale-api-management  
    threescale_component: system  
    threescale_component_element: smtp  
  ownerReferences:  
    - apiVersion: apps.3scale.net/v1alpha1  
      kind: APIManager  
      name: ddp-apimanager  
      uid: 38994f4f-ddba-4a39-a2ca-dddbbcc1f9cc  
      controller: true  
      blockOwnerDeletion: true  
data:  
  address: 'krrelay.corp.doosan.com'  
  authentication: 'plain'  
  domain: ''  
  openssl.verify.mode: 'none'  
  password: ''  
  port: '25'  
  username: ''
```