```
gcloud iam service-accounts create sa-sqlproxy
```
   

```
### sa에 권한 부여 필요??
```
   

```
gcloud iam service-accounts keys create key.json \  
  --iam-account sa-sqlproxy@laonpms.iam.gserviceaccount.com
```
   

```
kubectl create secret generic sqlproxy \  
--from-file=service_account.json=key.json
```
      

```
### deployment 수정 - sidecar 컨테이너 추가  
      - name: cloud-sql-proxy  
        image: gcr.io/cloudsql-docker/gce-proxy:1.17  
        command:  
        - "/cloud_sql_proxy"  
        - "-instances=laonpms:asia-northeast3:pms-db-dev=tcp:5432"  
        - "-credential_file=/secrets/service_account.json"  
        securityContext:  
          runAsNonRoot: true  
        volumeMounts:  
        - name: secret-sqlproxy  
          mountPath: /secrets/  
          readOnly: true
```
   

```
      volumes:  
      - name: secret-sqlproxy  
        secret:  
          secretName: sqlproxy
```