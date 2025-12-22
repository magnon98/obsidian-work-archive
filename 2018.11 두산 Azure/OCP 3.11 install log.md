```
$ sudo subscription-manager register --username=redhat@exntu.com --password=exntu~redhat --auto-attach  
$ sudo subscription-manager attach --pool=8a85f98b64f079fc01650fbc05ed3c89  
$ sudo subscription-manager repos \  
    --enable="rhel-7-server-rpms" \  
    --enable="rhel-7-server-extras-rpms" \  
    --enable="rhel-7-server-ose-3.11-rpms" \  
    --enable="rhel-7-server-ansible-2.6-rpms"
```
    
```
$ git clone [https://github.com/openshift/openshift-ansible.git](https://github.com/openshift/openshift-ansible.git)  
$ git checkout openshift-ansible-3.11.16-1  
$ ansible all -m ping -i inventory/ocp.bliex.io.cfg   
$ ansible-playbook -i inventory/ocp.bliex.io.cfg ./playbooks/prerequisites.yml  
$ ansible-playbook -i inventory/ocp.bliex.io.cfg ./playbooks/deploy_cluster.yml 
```
      

```
$ sudo htpasswd /etc/origin/master/htpasswd admin  
$ oc login -u admin -p admin.!  
$ oc login -u system:admin  
$ oc adm policy add-cluster-role-to-user cluster-admin admin  
$ oc login -u admin -p admin.!
```
    
```
$ for i in {001..020}; do sudo mkdir pv$i; sudo chmod 777 pv$i; done	
```
   

```
$ cat \<\<EOFF \> mkpv.sh  
#!/bin/bash
```
 
```
for i in {001..010}; do  
   PV=\$(cat \<\<EOF  
apiVersion: v1  
kind: PersistentVolume  
metadata:  
  name: pv\$i  
spec:  
 capacity:  
   storage: 10Gi  
 accessModes:  
   - ReadWriteOnce  
   - ReadWriteMany  
 persistentVolumeReclaimPolicy: Recycle  
 nfs:  
   server: 192.168.100.59  
   path: /exports/pv\$i  
EOF  
)  
   echo "\$PV" | oc create -f -  
done  
EOFF
```
 
```
$ chmod u+x mkpv.sh  
$ ./mkpv.sh
```
                     

```
$ cat inventory/ocp.bliex.io.cfg  
[OSEv3:children]  
masters  
nodes  
etcd
```
 
```
[OSEv3:vars]  
ansible_ssh_user=bliex  
ansible_become=true  
deployment_type=openshift-enterprise  
openshift_clock_enabled=true
```
 
```
openshift_release=v3.11  
openshift_pkg_version=-3.11.16  
openshift_image_tag=v3.11.16
```
   

```
openshift_master_api_port=8443  
openshift_master_console_port=8443  
openshift_master_cluster_hostname=m1.ocp.bliex.io  
openshift_master_cluster_public_hostname=m1.ocp.bliex.io  
openshift_master_cluster_method=native  
#openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider', 'filename': '/etc/origin/master/htpasswd'}]  
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider'}]
```
 
```
#openshift_router_selector='region=infra'  
#openshift_router_replicas=1
```
 
```
#openshift_registry_selector='region=infra'  
#openshift_registry_replicas=1
```
 
```
#os_sdn_network_plugin_name='redhat/openshift-ovs-multitenant'
```
 
```
#openshift_hosted_registry_cert_expire_days=1825  
#openshift_ca_cert_expire_days=1825  
#openshift_node_cert_expire_days=1825  
#openshift_master_cert_expire_days=1825  
#etcd_ca_default_days=1825
```
 
```
openshift_master_default_subdomain=app.ocp.bliex.io  
osm_default_node_selector="region=primary"
```
 
```
#os_firewall_use_firewalld=false
```
 
```
#openshift_use_crio=false  
#openshift_crio_enable_docker_gc=false
```
 
```
#template_service_broker_install=false
```
 
```
#ansible_service_broker_install=false
```
 
```
#openshift_metrics_install_metrics=true  
#openshift_metrics_start_cluster=true  
#openshift_metrics_image_prefix=registry.access.redhat.com:5000/openshift3/  
#openshift_metrics_master_url=https://dsdtpocm01.corp.doosan.com:8443  
#openshift_metrics_image_version=v3.9.31
```
 
```
#openshift_metrics_cassandra_pvc_size=10Gi  
#openshift_metrics_cassandra_storage_type=pv  
#openshift_metrics_cassandra_replicas=1  
#openshift_metrics_cassandra_nodeselector={"region":"infra"}  
#openshift_metrics_hawkular_replicas=1  
#openshift_metrics_hawkular_nodeselector={"region":"infra"}  
#openshift_metrics_heapster_nodeselector={"region":"infra"}  
#openshift_metrics_install_hawkular_agent=true  
#openshift_metrics_hawkular_hostname=hawkular-metrics.paas.corp.doosan.com  
#openshift_master_metrics_public_url=https://hawkular-metrics.paas.corp.doosan.com/hawkular/metrics
```
 
```
#openshift_logging_install_logging=true  
#openshift_logging_storage_kind=nfs  
#openshift_logging_storage_access_modes=['ReadWriteOnce']  
#openshift_logging_storage_host=dsdtpocr01.corp.doosan.com  
#openshift_logging_storage_nfs_directory=/nas-storage/logging  
#openshift_logging_storage_volume_name=logging-volume  
#openshift_logging_storage_volume_size=50Gi  
#openshift_enable_unsupported_configurations=True
```
   

```
#openshift_install_examples=true  
#openshift_examples_modify_imagestreams=true  
#oreg_url=registry.access.redhat.com/openshift3/ose-${component}:${version}  
#openshift_docker_additional_registries=registry.access.redhat.com  
#openshift_docker_insecure_registries=registry.access.redhat.com  
#openshift_docker_blocked_registries=docker.io  
#openshift_docker_options="--insecure-registry 172.30.0.0/16 -l warn --log-driver json-file --log-opt max-size=100M --log-opt max-file=10 "  
#openshift_node_kubelet_args={'pods-per-core': ['10'], 'max-pods': ['250'], 'image-gc-high-threshold': ['80'], 'image-gc-low-threshold': ['70']}
```
 
```
### Fix not meet requirement  
openshift_disable_check=docker_storage,memory_availability
```
   

```
oreg_auth_user=11351780|bliex  
oreg_auth_password=eyJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJkMmQxOWIxNGEwYjc0MDQ5OGJmNGE0NWFmYWE5NzUzZiJ9.hqIAIyf1lq5wD4xIRyzzC_DbnWNJxd3cyUVKpXjeRQ8dBKlNK9xqCDYUwcX9I9Z6oiX85NDDbF6f16ZUj47r-mSr_mNWk-9Z0691VdvRkSpBpEn9Ugwh2awwFtcnc-crV9xu05xeWARvj3N3qtUDm2yxFWHSppJI5Rt1m3hcd47x34WXE-240NSpqVlL2TOCp6ujGTLgMWRrcWv08f9q8_APVpWfVASzJl5cQ8pUbH8oQGtPkbL5TjViaEh-0lz-5nnpbMn04sDdNL-3FDeHnA_P4UoBfLNUTdm8OJJHUPyp1kYP6-wMATMUuj4ImCpj7BqaBzmCNN93XGSjzswkRZ1_Dnp__uV20SjOprlih4C94NO2VgYBchOkeVeEUZCJrBdtRRp9ToNTxpdy4iYtilVT3-3CPu1HlSLvPBW6vVFXdEUcoirJp91mwEp1-uQviOZlaxJC4UiLNM5TkKc4xrqDJRX7OxeH4g3T9xlBN87MQRwRLbace4PsJSah3yCxisxxdmul9CoQXdPz-Hq4_3tMAPdPTpp968-caBL0P2uaqo9WwCvN-bO5s-0KoxYCjAR3naiO_w230TI6LNFIAwrKLNbvXcGYTMxA_-8TA3wdhosD4KoKxo2rDGE21EkHQ7GY_2n7zyswmgmu0QadI5mKn73wJKeUHfSSHTqWqbo
```
    
```
[masters]  
m1.ocp.bliex.io  
m2.ocp.bliex.io  
m3.ocp.bliex.io  
   
   
# host group for etcd  
[etcd]  
m1.ocp.bliex.io  
m2.ocp.bliex.io  
m3.ocp.bliex.io  
   
   
# host group for nodes, includes region info  
[nodes]  
m1.ocp.bliex.io openshift_node_group_name='node-config-master'  
m2.ocp.bliex.io openshift_node_group_name='node-config-master'  
m3.ocp.bliex.io openshift_node_group_name='node-config-master'  
i1.ocp.bliex.io openshift_node_group_name='node-config-infra'  
i2.ocp.bliex.io openshift_node_group_name='node-config-infra'  
w1.ocp.bliex.io openshift_node_group_name='node-config-compute'  
w2.ocp.bliex.io openshift_node_group_name='node-config-compute'  
w3.ocp.bliex.io openshift_node_group_name='node-config-compute'
```