EFK 설치용 yaml 생성  
efk.yml

Prometheus / Grafana 설치 스크립트 추가  
monitoring.yml  
roles/monitoring/*

docker 버전을 1.13에서 17.03-ce로 변경  
diff --git a/roles/docker/defaults/main.yml b/roles/docker/defaults/main.yml  
index 9da348c..c3a7abf 100644  
--- a/roles/docker/defaults/main.yml  
+++ b/roles/docker/defaults/main.yml  
@@ -1,5 +1,5 @@  
---  
-docker_version: '1.13'  
+docker_version: 'stable'

EFK 스택 버전을 각각 5.4.0 및 1.24로 변경  
diff --git a/roles/download/defaults/main.yml b/roles/download/defaults/main.yml  
index d5c5ef7..453cc38 100644  
--- a/roles/download/defaults/main.yml  
+++ b/roles/download/defaults/main.yml  
@@ -89,13 +89,13 @@ kubednsautoscaler_image_repo: "gcr.io/google_containers/cluster-proportional-aut  
kubednsautoscaler_image_tag: "{{ kubednsautoscaler_version }}"  
test_image_repo: busybox  
test_image_tag: latest  
-elasticsearch_version: "v2.4.1"  
+elasticsearch_version: "v5.4.0-1"  
elasticsearch_image_repo: "gcr.io/google_containers/elasticsearch"  
elasticsearch_image_tag: "{{ elasticsearch_version }}"  
-fluentd_version: "1.22"  
+fluentd_version: "1.24"  
fluentd_image_repo: "gcr.io/google_containers/fluentd-elasticsearch"  
fluentd_image_tag: "{{ fluentd_version }}"  
-kibana_version: "v4.6.1"  
+kibana_version: "v5.4.0"  
kibana_image_repo: "gcr.io/google_containers/kibana"  
kibana_image_tag: "{{ kibana_version }}"
 
ElasticSearch 컨테이너의 vm.max_map_count 값 변경을 위해 initContainer 항목 추가.  
xms, xmx 값 변경.  
rbac옵션은 제거  
diff --git a/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-deployment.yml.j2 b/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-deployment.yml.j2  
index 6d5382e..1f9564a 100644  
--- a/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-deployment.yml.j2  
+++ b/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-deployment.yml.j2  
@@ -22,9 +22,19 @@ spec:  
version: "{{ elasticsearch_image_tag }}"  
kubernetes.io/cluster-service: "true"  
spec:  
+ initContainers:  
+ - name: init-sysctl  
+ image: busybox  
+ imagePullPolicy: IfNotPresent  
+ command: ["sysctl", "-w", "vm.max_map_count=262144"]  
+ securityContext:  
+ privileged: true  
containers:  
- image: "{{ elasticsearch_image_repo }}:{{ elasticsearch_image_tag }}"  
name: elasticsearch-logging  
+ env:  
+ - name: ES_JAVA_OPTS  
+ value: "-Xms1g -Xmx1g"  
resources:  
# need more cpu upon initialization, therefore burstable class  
limits:  
@@ -50,7 +60,3 @@ spec:  
volumes:  
- name: es-persistent-storage  
emptyDir: {}  
-{% if rbac_enabled %}  
- serviceAccountName: efk  
-{% endif %}  
-

ElasticSearch 에 nodePort 지정  
diff --git a/roles/kubernetes-apps/efk/elasticsearch/defaults/main.yml b/roles/kubernetes-apps/efk/elasticsearch/defaults/main.yml  
index d38ba6a..0b98993 100644  
--- a/roles/kubernetes-apps/efk/elasticsearch/defaults/main.yml  
+++ b/roles/kubernetes-apps/efk/elasticsearch/defaults/main.yml  
@@ -4,3 +4,4 @@ elasticsearch_mem_limit: 0M  
elasticsearch_cpu_requests: 100m  
elasticsearch_mem_requests: 0M  
elasticsearch_service_port: 9200  
+elasticsearch_node_port: 30503
 
```
diff --git a/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-service.yml.j2 b/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-service.yml.j2  
index b7558f9..90a9f5a 100644  
--- a/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-service.yml.j2  
+++ b/roles/kubernetes-apps/efk/elasticsearch/templates/elasticsearch-service.yml.j2  
@@ -9,10 +9,12 @@ metadata:  
     kubernetes.io/cluster-service: "true"  
     kubernetes.io/name: "Elasticsearch"  
 spec:  
+  type: NodePort  
   ports:  
-  - port: {{ elasticsearch_service_port }}  
+  - name: elasticsearch  
     protocol: TCP  
-    targetPort: db  
+    port: {{ elasticsearch_service_port }}  
+    targetPort: {{ elasticsearch_service_port }}  
+    nodePort: {{ elasticsearch_node_port }}  
   selector:  
     k8s-app: elasticsearch-logging
```

Kibana가 모든 가용한 IP를 통해 작동하도록 변경. nodePort 추가. rbac 삭제  
diff --git a/roles/kubernetes-apps/efk/kibana/defaults/main.yml b/roles/kubernetes-apps/efk/kibana/defaults/main.yml  
index baf07cd..a17843b 100644  
--- a/roles/kubernetes-apps/efk/kibana/defaults/main.yml  
+++ b/roles/kubernetes-apps/efk/kibana/defaults/main.yml  
@@ -4,4 +4,5 @@ kibana_mem_limit: 0M  
kibana_cpu_requests: 100m  
kibana_mem_requests: 0M  
kibana_service_port: 5601  
-kibana_base_url: "/api/v1/proxy/namespaces/kube-system/services/kibana-logging"  
+kibana_node_port: 30603  
+#kibana_base_url: "/api/v1/proxy/namespaces/kube-system/services/kibana-logging"  
diff --git a/roles/kubernetes-apps/efk/kibana/templates/kibana-deployment.yml.j2 b/roles/kubernetes-apps/efk/kibana/templates/kibana-deployment.yml.j2  
index c48413b..5c6a58e 100644  
--- a/roles/kubernetes-apps/efk/kibana/templates/kibana-deployment.yml.j2  
+++ b/roles/kubernetes-apps/efk/kibana/templates/kibana-deployment.yml.j2  
@@ -40,11 +40,9 @@ spec:  
- name: "KIBANA_BASE_URL"  
value: "{{ kibana_base_url }}"  
{% endif %}  
+ - name: "KIBANA_HOST"  
+ value: "0.0.0.0"  
ports:  
- - containerPort: 5601  
+ - containerPort: {{ kibana_service_port }}  
name: ui  
protocol: TCP  
-{% if rbac_enabled %}  
- serviceAccountName: efk  
-{% endif %}  
diff --git a/roles/kubernetes-apps/efk/kibana/templates/kibana-service.yml.j2 b/roles/kubernetes-apps/efk/kibana/templates/kibana-service.yml.j2  
index 241b896..53b4e72 100644  
--- a/roles/kubernetes-apps/efk/kibana/templates/kibana-service.yml.j2  
+++ b/roles/kubernetes-apps/efk/kibana/templates/kibana-service.yml.j2  
@@ -9,10 +9,13 @@ metadata:  
kubernetes.io/cluster-service: "true"  
kubernetes.io/name: "Kibana"  
spec:  
+ type: NodePort  
ports:  
- - port: {{ kibana_service_port }}  
+ - name: kibana  
protocol: TCP  
- targetPort: ui  
+ port: {{ kibana_service_port }}  
+ targetPort: {{ kibana_service_port }}  
+ nodePort: {{ kibana_node_port }}  
selector:  
k8s-app: kibana-logging