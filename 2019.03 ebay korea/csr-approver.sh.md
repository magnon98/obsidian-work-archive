```
* * * * * /bin/bash -c '/root/bin/csr_approver.sh | systemd-cat -t csr-approver'
```

```
#!/bin/bash
```
 
```
if [[ `oc whoami 2\>/dev/null` != "system:admin" ]]; then  
    echo "Error - Please login as system:admin"  
    exit 1  
fi
```
 
```
while [[ `oc get csr | grep Pending | wc -l` \> 0 ]]; do  
    oc get csr | grep Pending | awk '{print $1}' | xargs oc adm certificate approve 2\>&1  
    sleep 3  
done
```
 
```
if [[ `oc get csr | grep Approved | wc -l` \> 0 ]]; then  
    oc get csr | grep Approved | awk '{print $1}' | xargs oc delete csr  
fi
```

```
#!/bin/bash  
PENDING_SELECTOR='.items[] | select(.status == {}) | .metadata.name'  
APPROVED_SELECTOR='.items[] | select(.status != {}) | select(.status.conditions[].type == "Approved") | .metadata.name'
```
 
```
if [[ `oc whoami 2\>/dev/null` != "system:admin" ]]; then  
    echo "Error - Please login as system:admin"  
    exit 1  
fi
```
 
```
while [[ `oc get csr -o json | jq -r "$PENDING_SELECTOR" | wc -l` \> 0 ]]; do  
    oc get csr -o json | jq -r "$PENDING_SELECTOR" | xargs oc adm certificate approve  
    sleep 3  
done
```
 
```
if [[ `oc get csr -o json | jq -r "$APPROVED_SELECTOR" | wc -l` \> 0 ]]; then  
    oc get csr -o json | jq -r "$APPROVED_SELECTOR" | xargs oc delete csr  
fi
```