Repo : https://[five@tde.sktelecom.com](mailto:five@tde.sktelecom.com)/stash/scm/bef/bef-portal.git
   

Shell 1  
cd ./bef-portal-svc  
pwd  
# git checkout -- build.gradle  
#cat \<\<EOF | tee -a build.gradle  
#  
#apply plugin: 'war'  
#war {  
#    baseName = 'bef-portal-svc'  
#    version =  '0.1.1'  
#}  
#EOF  
/usr/lib/gradle/bin/gradle clean build  
# git checkout -- build.gradle  
Shell 2  
scp -i ~/.ssh/bef_dev_rsa ./builder/build/libs/bef-portal-svc-*.war bef@50.1.111.185:/opt/war_store/ROOT.war  
# ssh -i ~/.ssh/bef_dev_rsa bef@50.1.111.185 sudo systemctl restart tomcat