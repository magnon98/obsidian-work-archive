```
[OSEv3:children]  
nodes  
masters  
etcd  
#nfs
```
 
```
[OSEv3:vars]  
openshift_release="3.11"  
openshift_image_tag="v3.11.117"  
openshift_pkg_version=-3.11.117
```
 
```
#openshift_disable_check=memory_availability,disk_availability  
openshift_disable_check=memory_availability,disk_availability,docker_storage,docker_storage_driver,docker_image_availability,package_version,package_availability,package_update
```
 
```
openshift_clock_enabled=true  
openshift_enable_unsupported_configurations=true  
openshift_master_default_subdomain=app.ebaykorea.com
```
 
```
openshift_deployment_type=openshift-enterprise  
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider'}]
```
 
```
#openshift_master_htpasswd_file=/home/ebaycloud/htpasswd.openshift
```
 
```
openshift_master_cluster_method=native  
openshift_master_cluster_hostname=fusion-apigateway-internal.ebaykorea.com  
openshift_master_cluster_public_hostname=fusion-apigateway.ebaykorea.com                              
```
 
```
openshift_node_groups=[{'name': 'node-config-master', 'labels': ['node-role.kubernetes.io/master=true']}, {'name': 'node-config-infra', 'labels': ['node-role.kubernetes.io/infra=true']}, {'name': 'node-config-router', 'labels': ['node-role.kubernetes.io/router=true']}, {'name': 'node-config-compute', 'labels': ['node-role.kubernetes.io/compute=true'], 'edits': [{ 'key': 'kubeletArguments.pods-per-core','value': ['20']}]}]
```
 
```
openshift_master_api_port=443  
openshift_master_console_port=443
```
 
```
os_sdn_network_plugin_name=redhat/openshift-ovs-subnet  
openshift_master_pod_eviction_timeout=1m
```
 
```
openshift_master_named_certificates=[{"certfile": "/etc/origin/master/named_certificates/star.auction.co.kr.crt", "keyfile": "/etc/origin/master/named_certificates/star.auction.co.kr.key", "names": ["fusion-apigateway.ebaykorea.com"], "cafile": "/etc/origin/master/named_certificates/ca-bundle.crt"}]  
openshift_master_overwrite_named_certificates=true
```
 
```
# Configure logrotate scripts  
logrotate_scripts=[{"name": "syslog", "path": "/var/log/cron\n/var/log/maillog\n/var/log/messages\n/var/log/secure\n/var/log/spooler\n", "options": ["daily", "rotate 7","size 500M", "compress", "sharedscripts", "missingok"], "scripts": {"postrotate": "/bin/kill -HUP `cat /var/run/syslogd.pid 2\> /dev/null` 2\> /dev/null || true"}}]
```
   

```
## SDN  
osm_cluster_network_cidr=10.128.0.0/14  
openshift_portal_net=172.130.0.0/16  
#osm_host_subnet_length=8
```
 
```
openshift_ca_cert_expire_days=3650  
openshift_node_cert_expire_days=3650  
openshift_master_cert_expire_days=3650  
etcd_ca_default_days=3650  
openshift_hosted_registry_cert_expire_days=3650  
openshift_certificate_expiry_warning_days=2920  
openshift_certificate_expiry_fail_on_warn=2920
```
   

```
oreg_url=ecr.ebaykorea.com/openshift3/ose-${component}:${version}  
openshift_examples_modify_imagestreams=true  
osm_etcd_image=ecr.ebaykorea.com/openshift3/rhel7/etcd:3.2.22
```
 
```
#oreg_auth_user=test01@redhat.com  
#oreg_auth_password=test1234!
```
 
```
#openshift_docker_insecure_registries=ecr.ebaykorea.com  
openshift_docker_additional_registries=ecr.ebaykorea.com  
openshift_docker_blocked_registries=docker.io
```
   

```
openshift_docker_options="--insecure-registry 172.130.0.0/16 -l warn --log-driver json-file --log-opt max-size=10M --log-opt max-file=3"  
#openshift_docker_options="--selinux-enabled --insecure-registry 172.130.0.0/16 -l warn --log-driver json-file --log-opt max-size=10M --log-opt max-file=3"  
#openshift_docker_options="--insecure-registry 172.130.0.0/16 -l warn --log-driver json-file --log-opt max-size=10M --log-opt max-file=3"
```
   

```
## Prometheus Cluster monitoring after 3.11  
openshift_cluster_monitoring_operator_install=true  
openshift_cluster_monitoring_operator_prometheus_storage_capacity="50Gi"  
openshift_cluster_monitoring_operator_alertmanager_storage_capacity="2Gi"  
openshift_cluster_monitoring_operator_prometheus_storage_enabled=true  
openshift_cluster_monitoring_operator_alertmanager_storage_enabled=true
```
 
```
## Hawkular metrics and Metrics Server  
openshift_metrics_install_metrics=true  
openshift_metrics_server_install=true  
openshift_metrics_image_version=v3.11.117  
#openshift_metrics_cassandra_storage_type=dynamic  
openshift_metrics_cassandra_replicas=1  
openshift_metrics_hawkular_replicas=1  
openshift_metrics_cassandra_nodeselector={"node-role.kubernetes.io/infra":"true"}  
openshift_metrics_hawkular_nodeselector={"node-role.kubernetes.io/infra":"true"}  
openshift_metrics_heapster_nodeselector={"node-role.kubernetes.io/infra":"true"}  
openshift_metrics_image_prefix=ecr.ebaykorea.com/openshift3/
```
 
```
## Hawkular metrics NFS  
openshift_metrics_cassandra_pvc_size=200Gi  
openshift_metrics_cassandra_storage_type=pv  
openshift_metrics_storage_kind=nfs  
openshift_metrics_storage_access_modes=['ReadWriteOnce']  
openshift_metrics_storage_host=upimage.gmarket.nas  
openshift_metrics_storage_nfs_directory=/ifs/etc_service/api-gateway  
openshift_metrics_storage_volume_name=metrics  
openshift_metrics_storage_volume_size=200Gi  
openshift_metrics_storage_labels={'storage': 'metrics'}
```
 
```
## EFK  
openshift_logging_install_logging=true  
#openshift_logging_install_eventrouter=false  
openshift_logging_use_ops=false  
openshift_logging_es_cluster_size=1  
openshift_logging_es_memory_limit=6G  
openshift_logging_kibana_hostname=kibana.app.ebaykorea.com  
#openshift_logging_master_url=https://fusion-apigateway-internal.ebaykorea.com  
#openshift_logging_master_public_url=https://fusion-apigateway.ebaykorea.com  
openshift_logging_image_prefix=ecr.ebaykorea.com/openshift3/  
openshift_logging_es_pvc_dynamic=false  
openshift_logging_es_pvc_size=150Gi  
openshift_logging_es_pvc_selector={'storage': 'logging-es'}  
openshift_logging_image_version=v3.11.117  
openshift_logging_curator_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_kibana_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_es_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_eventrouter_nodeselector={'node-role.kubernetes.io/infra':'true'}  
openshift_logging_fluentd_memory_limit=512Mi  
openshift_logging_mux_memory_limit=256Mi
```
 
```
## webconsole  
openshift_web_console_install=true  
openshift_web_console_prefix=ecr.ebaykorea.com/openshift3/ose-  
openshift_cockpit_deployer_image=ecr.ebaykorea.com/openshift3/registry-console:v3.11.117
```
 
```
## Router   
openshift_hosted_router_selector='node-role.kubernetes.io/router=true'  
openshift_hosted_router_replicas=1
```
 
```
## Registry   
openshift_hosted_manage_registry=true                                                               
openshift_hosted_registry_selector='node-role.kubernetes.io/infra=true'  
openshift_hosted_registry_replicas=1
```
 
```
openshift_hosted_registry_pullthrough=true  
openshift_hosted_registry_acceptschema2=true  
openshift_hosted_registry_enforcequota=true
```
   

```
## Registry NFS  
openshift_hosted_registry_storage_kind=nfs  
openshift_hosted_registry_storage_access_modes=['ReadWriteMany']  
openshift_hosted_registry_storage_host=upimage.gmarket.nas  
openshift_hosted_registry_storage_nfs_directory=/ifs/etc_service/api-gateway  
openshift_hosted_registry_storage_volume_name=registry  
openshift_hosted_registry_storage_volume_size=100Gi
```
 
```
ansible_ssh_user=cpmadm  
ansible_become=true
```
 
```
## Service Catalog and Template Service Broker  
openshift_enable_service_catalog=false  
template_service_broker_install=false  
ansible_service_broker_install=false
```
 
```
openshift_enable_service_remove=true  
template_service_broker_remove=true  
ansible_service_broker_remove=true
```
   

```
[masters]  
apigateway01gm.gmarket.nh openshift_node_group_name='node-config-master'  
apigateway02gm.gmarket.nh openshift_node_group_name='node-config-master'  
apigateway03gm.gmarket.nh openshift_node_group_name='node-config-master'
```
   

```
#[nfs]  
#apigateway01gm.gmarket.nh openshift_node_group_name='node-config-master'
```
   

```
[etcd]  
apigateway01gm.gmarket.nh openshift_node_group_name='node-config-master'  
apigateway02gm.gmarket.nh openshift_node_group_name='node-config-master'  
apigateway03gm.gmarket.nh openshift_node_group_name='node-config-master'
```
   

```
[nodes]  
apigateway01gm.gmarket.nh openshift_node_group_name='node-config-master'  
apigateway02gm.gmarket.nh openshift_node_group_name='node-config-master'  
apigateway03gm.gmarket.nh openshift_node_group_name='node-config-master'  
apigateway04gm.gmarket.nh openshift_node_group_name='node-config-infra'  
apigateway05gm.gmarket.nh openshift_node_group_name='node-config-infra'  
apigateway06gm.gmarket.nh openshift_node_group_name='node-config-infra'  
apigateway07gm.gmarket.nh openshift_node_group_name='node-config-router'  
apigateway08gm.gmarket.nh openshift_node_group_name='node-config-router'  
apigateway09gm.gmarket.nh openshift_node_group_name='node-config-router'  
apigateway10gm.gmarket.nh openshift_node_group_name='node-config-compute'  
apigateway11gm.gmarket.nh openshift_node_group_name='node-config-compute'  
apigateway12gm.gmarket.nh openshift_node_group_name='node-config-compute'  
apigateway13gm.gmarket.nh openshift_node_group_name='node-config-compute'
```