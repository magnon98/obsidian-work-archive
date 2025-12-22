# cat /etc/ansible/hosts  
[OSEv3:children]  
masters  
nodes  
etcd
 
[OSEv3:vars]  
ansible_ssh_user=ocpadmin  
ansible_become=true  
deployment_type=openshift-enterprise  
openshift_clock_enabled=true
 
openshift_release=v3.9  
openshift_pkg_version=-3.9.31  
openshift_image_tag=v3.9.31
   

openshift_master_api_port=8443  
openshift_master_console_port=8443  
openshift_master_cluster_hostname=DSDTPOCM01.corp.doosan.com  
openshift_master_cluster_public_hostname=DSDTPOCM01.corp.doosan.com  
openshift_master_cluster_method=native  
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider', 'filename': '/etc/origin/master/htpasswd'}]
 
openshift_router_selector='region=infra'  
openshift_router_replicas=1
 
openshift_registry_selector='region=infra'  
openshift_registry_replicas=1
 
os_sdn_network_plugin_name='redhat/openshift-ovs-multitenant'
 
openshift_hosted_registry_cert_expire_days=1825  
openshift_ca_cert_expire_days=1825  
openshift_node_cert_expire_days=1825  
openshift_master_cert_expire_days=1825  
etcd_ca_default_days=1825
 
openshift_master_default_subdomain=paas.corp.doosan.com  
osm_default_node_selector="region=primary"
 
os_firewall_use_firewalld=false
 
openshift_use_crio=false  
openshift_crio_enable_docker_gc=false
 
template_service_broker_install=false
 
ansible_service_broker_install=false
   

openshift_logging_install_logging=true  
openshift_logging_storage_kind=nfs  
openshift_logging_storage_access_modes=['ReadWriteOnce']  
openshift_logging_storage_host=dsdtpocr01.corp.doosan.com  
openshift_logging_storage_nfs_directory=/nas-storage/logging  
openshift_logging_storage_volume_name=logging-volume  
openshift_logging_storage_volume_size=50Gi  
openshift_enable_unsupported_configurations=True
   

openshift_install_examples=true  
openshift_examples_modify_imagestreams=true  
oreg_url=registry.access.redhat.com/openshift3/ose-${component}:${version}  
openshift_docker_additional_registries=registry.access.redhat.com  
openshift_docker_insecure_registries=registry.access.redhat.com  
openshift_docker_blocked_registries=docker.io  
openshift_docker_options="--insecure-registry 172.30.0.0/16 -l warn --log-driver json-file --log-opt max-size=100M --log-opt max-file=10 "  
openshift_node_kubelet_args={'pods-per-core': ['10'], 'max-pods': ['250'], 'image-gc-high-threshold': ['80'], 'image-gc-low-threshold': ['70']}
 
[masters]  
DSDTPOCM01.corp.doosan.com openshift_ip=10.231.107.231 openshift_public_ip=10.231.107.231 openshift_hostname=DSDTPOCM01.corp.doosan.com openshift_public_hostname=DSDTPOCM01.corp.doosan.com
 
[etcd]  
DSDTPOCM01.corp.doosan.com openshift_ip=10.231.107.231 openshift_public_ip=10.231.107.231 openshift_hostname=DSDTPOCM01.corp.doosan.com openshift_public_hostname=DSDTPOCM01.corp.doosan.com
 
[nodes]  
DSDTPOCM01.corp.doosan.com openshift_ip=10.231.107.231 openshift_public_ip=10.231.107.231 openshift_hostname=DSDTPOCM01.corp.doosan.com openshift_public_hostname=DSDTPOCM01.corp.doosan.com openshift_node_labels="{'region': 'master', 'zone': 'default'}"  
DSDTPOCR01.corp.doosan.com openshift_ip=10.231.107.234 openshift_public_ip=10.231.107.234 openshift_hostname=DSDTPOCR01.corp.doosan.com openshift_public_hostname=DSDTPOCR01.corp.doosan.com openshift_node_labels="{'region': 'infra', 'zone': 'infra'}"  
DSDTPOCN01.corp.doosan.com openshift_ip=10.231.107.232 openshift_public_ip=10.231.107.232 openshift_hostname=DSDTPOCN01.corp.doosan.com openshift_public_hostname=DSDTPOCN01.corp.doosan.com openshift_node_labels="{'region': 'primary', 'zone': 'service'}"  
DSDTPOCN02.corp.doosan.com openshift_ip=10.231.107.233 openshift_public_ip=10.231.107.233 openshift_hostname=DSDTPOCN02.corp.doosan.com openshift_public_hostname=DSDTPOCN02.corp.doosan.com openshift_node_labels="{'region': 'primary', 'zone': 'service'}"