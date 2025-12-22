```
# cat useradd.sh  
#!/bin/sh  
##########################################################  
# useradd script  
# 2016.11.24  
# env_user 부분은 상황에 맞추어 수정하여 사용 하도록 하세요.  
##########################################################
```
 
```
USER_ID="skt_account"  
USER_PW="mccenter07!"  
USER_HOME="/home/skt_account"
```
 
```
init_var ()  
{  
        echo "function : Deploy Start"  
        echo "-------------------------------"
```
 
```
        unset LANG  
        LANG=C  
        TMOUT=0  
}
```
 
```
make_user ()  
{  
        echo "function : Make $USER_ID"  
        echo "-------------------------------"  
        useradd -d $USER_HOME -s "/bin/bash" -m $USER_ID  
        echo $USER_PW | passwd --stdin $USER_ID 1\>&-  
        gpasswd -a $USER_ID wheel
```
 
```
        echo "" \>\> /etc/sudoers  
        echo "#$USER_ID" \>\> /etc/sudoers  
        echo "$USER_ID ALL=NOPASSWD: ALL" \>\> /etc/sudoers  
        echo "" \>\> /etc/sudoers  
        echo "Defaults:$USER_ID !requiretty" \>\> /etc/sudoers  
}
```
 
```
env_user ()  
{  
        echo "function : Make environment of $USER_ID"  
        echo "-------------------------------"
```
 
```
        chage -E -1 -I 0 -m 0 -M 99999 $USER_ID || chage -E never -I 0 -m 0 -M 99999 $USER_ID  
        su - $USER_ID -c "umask 022; unset LANG; LANG=C; touch $USER_HOME/.bash_profile; echo export PATH=$PATH:/usr/bin:/usr/sbin:/usr/local/bin:/etc:. \>\> $USER_HOME/.bash_profile"  
}
```
 
```
#---------------------------------------  
clear
```
 
```
init_var
```
 
```
make_user
```
 
```
env_user
```