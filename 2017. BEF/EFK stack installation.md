```
fluentd  
$ curl -L [https://toolbelt.treasuredata.com/sh/install-redhat-td-agent2.sh](https://toolbelt.treasuredata.com/sh/install-redhat-td-agent2.sh) | sh  
$ sudo systemctl start td-agent  
$ sudo systemctl status td-agent  
$ sudo systemctl enable td-agent
```
   

```
$ sudo vi /etc/td-agent/td-agent.conf  
# collect the dmesg output  
\<source\>  
  type syslog  
  port 42185  
  tag syslog  
\</source\>  
\<match syslog.**\>  
  type elasticsearch  
  logstash_format true #Kibana understands only logstash format  
  flush_interval 10s # for testing  
\</match\>
```
   

```
elastic search  
$ wget [https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.3.noarch.rpm](https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.3.noarch.rpm)  
$ sudo rpm -ivh elasticsearch-1.7.3.noarch.rpm  
$ sudo systemctl start elasticsearch  
$ sudo systemctl status elasticsearch  
$ sudo systemctl enable elasticsearch  
$ sudo vi /etc/elasticsearch/elasticsearch.yml  
node.master: true  
node.data: true  
index.number_of_shards: 1  
index.number_of_replicas: 0  
path.data: /tmp/es_data
```