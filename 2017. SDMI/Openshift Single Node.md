Method 1  
$ docker run -d --name "origin" \  
--privileged --pid=host --net=host \  
-v /:/rootfs:ro -v /var/run:/var/run:rw -v /sys:/sys -v /sys/fs/cgroup:/sys/fs/cgroup:rw \  
-v /var/lib/docker:/var/lib/docker:rw \  
-v /var/lib/origin/openshift.local.volumes:/var/lib/origin/openshift.local.volumes:rslave \  
openshift/origin start
 
Method 2
 
1. 릴리즈 버전 다운로드 ([https://github.com/openshift/origin/releases/download/v3.6.0/openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit.tar.gz](https://github.com/openshift/origin/releases/download/v3.6.0/openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit.tar.gz))
 
$ tar zxf openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit.tar.gz  
$ cd openshift-origin-client-tools-v3.6.0-c4dd4cf-linux-64bit  
$ export PATH=`pwd`:$PATH  
$ sudo openshift start  
$ export KUBECONFIG=`pwd`/openshift.local.config/master/admin.kubeconfig  
$ export CURL_CA_BUNDLE=`pwd`/openshift.local.config/master/ca.crt  
$ sudo chmod +r `pwd`/openshift.local.config/master/admin.kubeconfig