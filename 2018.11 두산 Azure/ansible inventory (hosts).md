```
[OSEv3:children]  
masters  
nodes  
etcd  
new_nodes
```
 
```
# Set variables common for all OSEv3 hosts  
[OSEv3:vars]
```
 
```
ansible_ssh_user=root  
ansible_user=root  
openshift_release=v3.11.43  
openshift_image_tag=v3.11.43  
openshift_pkg_version=-3.11.43  
ansible_become=yes  
openshift_deployment_type=openshift-enterprise  
oreg_url=registry.redhat.io/openshift3/ose-${component}:${version}  
#oreg_auth_password={{ lookup('env','rh_user_pass') }}  
oreg_auth_password='J@$m!nAl@d1n'  
oreg_auth_user='dsocpadmin'  
openshift_examples_modify_imagestreams=true  
openshift_master_htpasswd_users={'admin': '$apr1$N7LYwSJU$GYWHhjuDtAcNo/T2dhi/1/'}  
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider'}]  
openshift_disable_check=docker_storage  
osm_default_node_selector='node-role.kubernetes.io/compute=true'  
openshift_node_groups=[{'name': 'node-config-router', 'labels': ['node-role.kubernetes.io/router=true']}, {'name': 'node-config-master', 'labels': ['node-role.kubernetes.io/master=true']}, {'name': 'node-config-infra', 'labels': ['node-role.kubernetes.io/infra=true',]},{'name': 'node-config-compute', 'labels': ['node-role.kubernetes.io/compute=true']}]  
openshift_registry_selector='node-role.kubernetes.io/infra=true'  
openshift_router_selector='node-role.kubernetes.io/router=true'  
os_sdn_network_plugin_name='redhat/openshift-ovs-subnet'  
os_firewall_use_firewalld=True  
openshift_use_dnsmasq=True  
openshift_master_cluster_method=native  
openshift_master_cluster_hostname=ddp-master-lb.d-platform.doosan.com  
openshift_master_cluster_public_hostname=d-platform.doosan.com  
openshift_master_default_subdomain=apps.d-platform.doosan.com  
openshift_master_api_port=443  
openshift_master_console_port=443
```
 
```
openshift_cloudprovider_kind=azure  
openshift_cloudprovider_azure_client_id="221d1368-bfee-4338-85f4-6bb3521dbfee"  
openshift_cloudprovider_azure_client_secret="4bb8c6a6-a4e8-411e-8d67-804f89af995c"  
openshift_cloudprovider_azure_tenant_id="9d1b3610-9ab0-42d5-93aa-46150d723d87"  
openshift_cloudprovider_azure_subscription_id="ec63dca7-a974-4aab-841c-cb3f1c785f37"
```
   

```
openshift_cloudprovider_azure_resource_group="DDPPRODRG"  
openshift_cloudprovider_azure_cloud=AzurePublicCloud  
openshift_cloudprovider_azure_location=koreacentral  
openshift_cloudprovider_azure_vnet_name=ddpprodnet  
openshift_cloudprovider_azure_security_group_name=ddp-app-nsg  
openshift_cloudprovider_azure_availability_set_name=ddp-app-av  
osm_controller_args={'cloud-provider': ['azure'], 'cloud-config': ['/etc/origin/cloudprovider/azure.conf']}  
osm_api_server_args={'cloud-provider': ['azure'], 'cloud-config': ['/etc/origin/cloudprovider/azure.conf']}  
openshift_node_kubelet_args={'cloud-provider': ['azure'], 'cloud-config': ['/etc/origin/cloudprovider/azure.conf'], 'enable-controller-attachdetach': ['true']}  
openshift_hosted_router_replicas=3  
#openshift_node_local_quota_per_fsgroup=512Mi  # \<--please confirm.  
#template_service_broker_install=false  
#ansible_service_broker_install=false
```
    
```
#Registry  
openshift_hosted_registry_routehost=registry.d-platform.doosan.com  
openshift_hosted_manage_registry=true  
openshift_hosted_registry_replicas=2  
openshift_hosted_registry_selector='node-role.kubernetes.io/infra=true'  
openshift_hosted_registry_storage_kind=object  
openshift_hosted_registry_storage_provider=azure_blob  
openshift_hosted_registry_storage_azure_blob_accountname=ddpdockerregistry  
openshift_hosted_registry_storage_azure_blob_accountkey="9NJjhdW3L9yShdt/NeG8xR+jwqfDIOasAWuPAiZ7SyW43drBW0G3ZX+TXALIjjLvaI6WymovYmgKCL44HfuxMQ=="  
openshift_hosted_registry_storage_azure_blob_container=registry  
openshift_hosted_registry_storage_azure_blob_realm=core.windows.net
```
   

```
#Metrics  
openshift_cluster_monitoring_operator_install=true  
openshift_cluster_monitoring_operator_prometheus_storage_enabled=true  
openshift_cluster_monitoring_operator_alertmanager_storage_enabled=true  
openshift_cluster_monitoring_operator_prometheus_storage_capacity=50Gi  
openshift_cluster_monitoring_operator_alertmanager_storage_capacity=3Gi  
openshift_metrics_duration=2  
openshift_metrics_cassandra_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_metrics_cassandra_replicas=2  
openshift_metrics_install_metrics=true  
openshift_metrics_cassandra_storage_type=dynamic  
openshift_metrics_hawkular_replicas=2  
#openshift_metrics_heapster_standalone=true  
openshift_metrics_heapster_nodeselector={'node-role.kubernetes.io/infra':'true'}  
#openshift_metrics_heapster_nodeselector={'node-role.kubernetes.io/infra':'true'}
```
 
```
##Logging  
openshift_logging_install_logging=True  
openshift_logging_storage_kind=dynamic  
openshift_logging_es_cluster_size=3  
#openshift_logging_es_ops_pvc_size=20Gi  
openshift_logging_es_pvc_size=100Gi  
openshift_logging_elasticsearch_pvc_dynamic=true  
openshift_logging_elasticsearch_pvc_size=100Gi  
openshift_logging_kibana_hostname=logs.d-platform.doosan.com
```
   

```
openshift_logging_curator_cpu_request=500m  
openshift_logging_curator_ops_cpu_request=50m  
openshift_logging_kibana_cpu_request=50m  
openshift_logging_kibana_proxy_cpu_request=50m  
openshift_logging_kibana_ops_cpu_request=50m  
openshift_logging_kibana_ops_proxy_cpu_request=50m  
openshift_logging_fluentd_cpu_request=50m  
openshift_logging_es_cpu_request=500m  
openshift_logging_es_ops_cpu_request=250m  
openshift_logging_mux_cpu_request=50m
```
 
```
openshift_logging_curator_memory_limit=256Mi  
openshift_logging_curator_ops_memory_limit=256Mi  
openshift_logging_kibana_memory_limit=450Mi  
openshift_logging_kibana_proxy_memory_limit=64Mi  
openshift_logging_kibana_ops_memory_limit=300Mi  
openshift_logging_kibana_ops_proxy_memory_limit=64Mi  
openshift_logging_fluentd_memory_limit=512Mi  
openshift_logging_es_memory_limit=4Gi  
openshift_logging_es_ops_memory_limit=2Gi  
openshift_logging_mux_memory_limit=256Mi
```
 
```
#openshift_logging_nodeselector='node-role.kubernetes.io/infra'  
openshift_logging_curator_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_curator_ops_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_kibana_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_kibana_ops_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_es_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_es_ops_nodeselector={'node-role.kubernetes.io/infra':'true'}
```
   

```
#To choose the which storage to use (Managed or Unmanaged)  
openshift_storageclass_parameters={'kind': 'Managed', 'storageaccounttype': 'Standard_LRS'} # need to check with customer...
```
   

```
# override the default controller lease ttl  
#osm_controller_lease_ttl=30
```
 
```
#openshift_node_groups: [{'name': 'node-config-master', 'labels': ['noderole.kubernetes.io/master=true']},{'name': 'node-config-infra', 'labels': ['noderole.kubernetes.io/infra=true']},{'name': 'node-config-compute', 'labels': ['noderole.kubernetes.io/compute=true']},{'name': 'node-config-infra-logging', 'labels':['node-role.kubernetes.io/infra-logging=true']}, {'name': 'node-config-infraregistry','labels': ['node-role.kubernetes.io/infra-registry=true']}]
```
 
```
#audit  
openshift_master_audit_config={"enabled": true, "auditFilePath": "/var/log/oscp-audit/-oscp-audit.log", "maximumFileRetentionDays": 14, "maximumFileSizeMegabytes": 500, "maximumRetainedFiles": 5, "policyFile": "/etc/security/adv-audit.yaml", "logFormat":"json"}
```
   

```
# host group for masters  
[masters]  
ddp-master-01.internal.cloudapp.net  
ddp-master-02.internal.cloudapp.net  
ddp-master-03.internal.cloudapp.net
```
 
```
# host group for etcd  
[etcd]  
ddp-master-01.internal.cloudapp.net  
ddp-master-02.internal.cloudapp.net  
ddp-master-03.internal.cloudapp.net
```
   

```
# host group for nodes  
[nodes]  
ddp-master-01.internal.cloudapp.net openshift_node_group_name="node-config-master"  
ddp-master-02.internal.cloudapp.net openshift_node_group_name="node-config-master"  
ddp-master-03.internal.cloudapp.net openshift_node_group_name="node-config-master"  
#ddp-app-01.internal.cloudapp.net openshift_node_group_name="node-config-compute"  
#ddp-app-02.internal.cloudapp.net openshift_node_group_name="node-config-compute"  
#ddp-app-04.internal.cloudapp.net openshift_node_group_name="node-config-compute"  
ddp-infra-01.internal.cloudapp.net openshift_node_group_name="node-config-infra"  
ddp-infra-02.internal.cloudapp.net openshift_node_group_name="node-config-infra"  
ddp-router-01.internal.cloudapp.net openshift_node_group_name="node-config-router"  
ddp-router-02.internal.cloudapp.net openshift_node_group_name="node-config-router"  
ddp-router-03.internal.cloudapp.net openshift_node_group_name="node-config-router"  
ddp-appnode-01.internal.cloudapp.net openshift_node_group_name="node-config-compute"  
ddp-appnode-02.internal.cloudapp.net openshift_node_group_name="node-config-compute"  
ddp-appnode-03.internal.cloudapp.net openshift_node_group_name="node-config-compute"  
ddp-appnode-04.internal.cloudapp.net openshift_node_group_name="node-config-compute"  
ddp-devnode-01.internal.cloudapp.net openshift_node_group_name="node-config-compute"
```
 
```
[new_nodes]
```