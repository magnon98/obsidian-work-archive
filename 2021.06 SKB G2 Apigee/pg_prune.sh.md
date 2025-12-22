```
#!/bin/bash
```
 
```
ORG=${1:-undefined}  
ENV=${2:-undefined}
```
 
```
DISK_THRESHOLD=${3:-undefined}  
RETENTION_PERIOD=${4:-undefined}
```
 
```
LOG_FILE=$(realpath $(dirname $0))/pg_prune.log
```
 
```
echo $ORG $ENV $DISK_THRESHOLD $RETENTION_PERIOD
```
 
```
if [[ $RETENTION_PERIOD == "undefined" ]]; then  
        echo not enough arguments  
        exit 1  
fi
```
 
```
echo "==============================================================="  
date | tee -a $LOG_FILE  
echo - ORG: $ORG | tee -a $LOG_FILE  
echo - ENV: $ENV | tee -a $LOG_FILE  
echo - DISK_THRESHOLD: $DISK_THRESHOLD | tee -a $LOG_FILE  
echo - RETENTION_PERIOD: $RETENTION_PERIOD | tee -a $LOG_FILE  
echo
```
 
```
DISK_USAGE=$(df -hT /opt/apigee | tail -n 1 | awk '{print $6}' | sed 's/%//')
```
 
```
while [[ $(( $DISK_USAGE - $DISK_THRESHOLD )) \> 0 ]] && [[ $RETENTION_PERIOD \> 0 ]]; do  
    echo 'Disk Usage - '$DISK_USAGE'% \> '$DISK_THRESHOLD'% - pruning pg data older than '$RETENTION_PERIOD' day(s).'
```
 
```
    /opt/apigee/apigee-service/bin/apigee-service apigee-postgresql pg-data-purge $ORG $ENV $RETENTION_PERIOD | tee -a $LOG_FILE
```
 
```
    RETENTION_PERIOD=$((RETENTION_PERIOD - 1))  
    DISK_USAGE=$(df -hT /opt/apigee | tail -n 1 | awk '{print $6}' | sed 's/%//')  
    sleep 5  
done
```