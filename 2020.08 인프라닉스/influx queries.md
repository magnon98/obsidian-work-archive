```
$ influx -host 112.175.115.243 -port 18086 -execute "show databases"  
name: databases  
name  
----  
cf_metric_db  
container_metric_db  
_internal  
bosh_metric_db
```
   

```
$ influx -host 112.175.115.243 -port 18086 -database 'container_metric_db' -execute "show measurements"  
name: measurements  
name  
----  
container_metrics
```
      

```
$ influx -host 112.175.115.243 -port 18086 -database 'container_metric_db' -execute "show tag keys from container_metrics"  
name: container_metrics  
tagKey  
------  
application_id  
application_index  
application_name  
application_url  
cell_ip  
container_id  
container_interface  
device  
machine  
name  
type
```
       
```
$ influx -host 112.175.115.243 -port 18086 -database 'container_metric_db' -execute "show tag values from container_metrics with key = \"name\""  
name: container_metrics  
key     value  
---     -----  
name    cpu_usage_total  
name    disk_usage  
name    load_average  
name    memory_usage  
name    rx_bytes  
name    rx_dropped  
name    rx_errors  
name    tx_bytes  
name    tx_dropped  
name    tx_errors
```
    
```
$ influx -host 112.175.115.243 -port 18086 -database 'container_metric_db' -execute "select * from container_metrics where time \> now() - 10m and \"name\" = 'cpu_usage_total'"  
name: container_metrics  
time                app_disk    app_mem    application_id                       application_index application_name  application_url                         cell_ip     container_id                                                                            container_interface device machine                              name            type value  
----                --------    -------    --------------                       ----------------- ----------------  ---------------                         -------     ------------                                                                            ------------------- ------ -------                              ----            ---- -----  
1606734430238252651                                                                                                                                         10.20.1.116 /system.slice/garden.service/garden                                                                                5548e435-6595-41cf-82d3-890251fc9dcf cpu_usage_total      0  
1606734430429227104 1073741824  134217728  b0042e86-e362-4c54-9011-845f17052d12 0                 cf-ex-phpmyadmin  cf-ex-phpmyadmin.spaasta.com            10.20.1.117 /garden/5dc1d26b-53f7-44c5-727a-54cf                                                    wgf3ebanb05n-0             adf5468a-d97e-41cf-865e-5811ca44a52b cpu_usage_total      61.722608251  
1606734430446993936 1073741824  1073741824 7c5e6c41-f4b5-453c-8167-232eebefaade 0                 test111           test111.spaasta.com                     10.20.1.158 /garden/c1442bff-e381-43a3-6eaf-b71f                                                    wgf4bimq5951-0             749916c0-a999-4b66-8298-59709957f7bd cpu_usage_total      1039.514141548  
1606734430492082128 1073741824  1073741824 9a913249-311a-484a-82c2-951c04cece90 0                 testapp3-GREEN    testapp3-green.spaasta.com              10.20.1.159 /system.slice/garden.service/garden/ea39d887-add8-4239-6b64-34d5                        wgf592le6nk8-0             6d9c82a1-474d-4bb4-b1ef-64dc427e29e5 cpu_usage_total      4280.308168004  
1606734430553945385 134217728   536870912  78f33cfe-139c-4498-b210-b36b5764f4eb 0                 istusersample     istusersample.spaasta.com               10.20.1.116 /system.slice/garden.service/garden/1f12c54d-daca-476b-5857-db8f                        wgf2mgtnsn6c-0             5548e435-6595-41cf-82d3-890251fc9dcf cpu_usage_total      27.241383867
```
    
```
$ influx -host 112.175.115.243 -port 18086 -database 'container_metric_db' -execute "select application_id, application_name, \"name\", type, value  from container_metrics where time \> now() - 10m and \"name\" = 'cpu_usage_total'"
```