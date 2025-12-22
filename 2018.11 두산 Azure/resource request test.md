```
oc label node ddp-app-01 optype=test
```
 
```
oc new-project \<request-test\>
```
 
```
oc annotate ns \<request-test\> openshift.io/node-selector='optype=test'
```
 
```
oc new-app centos/ruby-25-centos7~https://github.com/sclorg/ruby-ex.git
```
   

```
# CPU request test  
oc set resources dc/ruby-ex --requests=cpu=1,memory=100Mi --limits=cpu=2,memory=1Gi  
oc scale dc/ruby-ex --replicas=2
```
   

```
# Memory request test  
oc set resources dc/ruby-ex --requests=cpu=100m,memory=4Gi --limits=cpu=1,memory=6Gi  
oc scale dc/ruby-ex --replicas=2
```