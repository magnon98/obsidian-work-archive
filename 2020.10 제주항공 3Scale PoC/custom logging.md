```
Logging Policy
```
 
```
custom logging format:
```
 
```
[{{time_local}}] [{{http_x_forwarded_for}}] {{host}}:{{server_port}} {{remote_addr}}:{{remote_port}} \"{{request}}\" {{status}} {{body_bytes_sent}} ({{request_time}}) {{post_action_impact}}
```