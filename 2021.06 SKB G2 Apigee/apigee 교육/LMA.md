```
transaction log
```

```
apigee의 MessageLogging policy 에서 /opt/apigee/var/log/edge-message-processor/messagelogging/media/*/SF-Postflow/*/ML-ELK-Log/elk.log 파일로 저장
```

```
FileBeat가 elk.log 파일을 Kafka에 전달
```

```
이후 Kafka --\> LogStash --\> ElasticSearch
```
   

```
metric
```

```
각 노드에서 telegraf가 os 메트릭 수집하여 kafka에 전달
```

```
Metricbeat가 각 컴포넌트의 health check하여 kafka에 전달
```

```
이후 kafka --\> LogStash / Telegraf --\> influxdb --\> grafana
```