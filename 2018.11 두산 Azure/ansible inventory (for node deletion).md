```
[OSEv3:children]  
nodes
```
 
```
[OSEv3:vars]  
ansible_ssh_user=root  
ansible_user=root  
openshift_release=v3.11.43  
openshift_image_tag=v3.11.43  
openshift_pkg_version=-3.11.43  
ansible_become=yes  
openshift_deployment_type=openshift-enterprise
```
 
```
# host group for nodes  
[nodes]  
ddp-devnode-01.internal.cloudapp.net openshift_node_group_name="node-config-compute"
```
       
```
이 yaml로 uninstall playbook 수행 후 oc delete node  
이렇게 해야 인스턴스 재활용이 가능해짐.
```