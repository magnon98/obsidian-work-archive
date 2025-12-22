```
echo 'conf_cache_second.level.cache.element.max.size.in.bytes=3145728
```
 
```
bin_setenv_min_mem=4096m  
bin_setenv_max_mem=4096m  
bin_setenv_meta_space_size=1024m' | sudo -u apigee tee /opt/apigee/customer/application/message-processor.properties
```