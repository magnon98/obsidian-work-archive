scp -vvv  
-o ProxyCommand="ssh -vvv -W %h:%p -p $INFRANICS_BASTION_SSH_PORT -i infranics_bastion_rsa $INFRANICS_BASTION_USER@$INFRANICS_BASTION_HOST"
 
-i infranics_vm_rsa -r ./build/* $INFRANICS_VM_USER@$INFRANICS_VM_HOST:$INFRANICS_VM_CPM_UI_PATH