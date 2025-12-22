oc adm top node
      

for NODE in `oc get node -o name -l node-role.kubernetes.io/compute=true`; do echo -e "\n\n\n$NODE"; oc describe $NODE | grep -A5 "Allocated resources:"; done