```
# fdisk /dev/sdc  
g  
n  
w
```
   

```
# xe sr-create name-label=\<Storage ID\> \  
    shared=false \  
    device-config:device=\<Path of the Storage device\> \  
    type=lvm \  
    content-type=user
```
   

```
### ex 1  
# xe sr-create name-label=ssd \  
    shared=false \  
    device-config:device=/dev/sdc \  
    type=lvm \  
    content-type=user
```
 
```
### ex 2 - thin provisioning 사용을 위해서는 type을 ext 로 지정해야 함.  
# xe sr-create name-label=ssd \  
    shared=false \  
    device-config:device=/dev/sdc \  
    type=ext \  
    content-type=user
```