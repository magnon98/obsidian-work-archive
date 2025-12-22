```
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
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider'}]
```
 
```
openshift_master_default_subdomain=app.ocp.bliex.io  
osm_default_node_selector="region=primary"
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
m1.ocp.bliex.io openshift_node_group_name='node-config-master'  openshift_node_labels="{'region': 'master',  'zone': 'default'}"  
m2.ocp.bliex.io openshift_node_group_name='node-config-master'  openshift_node_labels="{'region': 'master',  'zone': 'default'}"  
m3.ocp.bliex.io openshift_node_group_name='node-config-master'  openshift_node_labels="{'region': 'master',  'zone': 'default'}"  
i1.ocp.bliex.io openshift_node_group_name='node-config-infra'   openshift_node_labels="{'region': 'infra',   'zone': 'default'}"  
i2.ocp.bliex.io openshift_node_group_name='node-config-infra'   openshift_node_labels="{'region': 'infra',   'zone': 'default'}"  
w1.ocp.bliex.io openshift_node_group_name='node-config-compute' openshift_node_labels="{'region': 'primary', 'zone': 'default'}"  
w2.ocp.bliex.io openshift_node_group_name='node-config-compute' openshift_node_labels="{'region': 'primary', 'zone': 'default'}"  
w3.ocp.bliex.io openshift_node_group_name='node-config-compute' openshift_node_labels="{'region': 'primary', 'zone': 'default'}"
```