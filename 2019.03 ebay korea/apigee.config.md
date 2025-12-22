```
### [https://docs.apigee.com/private-cloud/v4.19.01/edge-configuration-file-reference](https://docs.apigee.com/private-cloud/v4.19.01/edge-configuration-file-reference)
```
 
```
# IP address or DNS name of nodes.  
DS1=192.168.100.90      # ZooKeeper, Cassandra  
DS2=192.168.100.91      # ZooKeeper, Cassandra  
DS3=192.168.100.92      # ZooKeeper, Cassandra  
RMP1=192.168.100.93     # Router, Message Processor  
RMP2=192.168.100.94     # Router, Message Processor  
QS1=192.168.100.95      # Qpid  
QS2=192.168.100.96      # Qpid  
PG1=192.168.100.97      # Postgres  
PG2=192.168.100.98      # Postgres  
MS1=192.168.100.99      # Management Server, OpenLDAP, UI
```
      

```
# Must resolve to IP address or DNS name of host - not to 127.0.0.1 or localhost.  
HOSTIP=$(hostname -i)
```
 
```
# Specify "y" to check that the system meets the CPU and memory requirements  
# for the component being installed. See Installation Requirements for requirements  
# for each component. The default value is "n" to disable check.  
ENABLE_SYSTEM_CHECK=n
```
 
```
# When "hostname -i" returns multiple IP addresses,  
# set to "y", to have the installer prompt you to select the IP address to use.  
ENABLE_DYNAMIC_HOSTIP=n
```
      

```
# Set Edge sys admin credentials.  
ADMIN_EMAIL=magnon@bliex.com  
APIGEE_ADMINPW=...............    # If omitted, you are prompted for it.
```
 
```
# Location of Edge license file.  
LICENSE_FILE=/opt/installers/license.txt
```
      

```
# Management Server information.  
MSIP=$MS1    # IP or DNS name of Management Server node.
```
 
```
# Specify the port the Management Server listens on for API calls.  
# APIGEE_PORT_HTTP_MS=8080    # Default is 8080.
```
      

```
#  
# OpenLDAP information.  
#  
# Set to y if you are connecting to a remote LDAP server.  
# If n, Edge installs OpenLDAP when it installs the Management Server.  
USE_LDAP_REMOTE_HOST=n
```
 
```
# Specify OpenLDAP without replication, 1, or with replication, 2.  
LDAP_TYPE=1
```
 
```
# If connecting to remote OpenLDAP server, specify the IP/DNS name and port.  
# LDAP_HOST=$MS1    # IP or DNS name of OpenLDAP node.  
# LDAP_PORT=10389   # Default is 10389.  
APIGEE_LDAPPW=...............
```
 
```
# Set only if using replication.  
# LDAP_SID=1    # Unique ID for this LDAP server.  
# LDAP_PEER=    # IP or DNS name of LDAP peer.
```
      

```
# The Message Processor and Router pod.  
MP_POD=gateway
```
 
```
# The name of the region, corresponding to the data center name.  
REGION=dc-1 # Use dc-1 unless installing in a  
            # multi-data center environment.
```
       
```
# ZooKeeper information.  
# See table below if installing in a multi-data center environment.  
ZK_HOSTS="$DS1 $DS2 $DS3"         # IP/DNS names of all ZooKeeper nodes.  
ZK_CLIENT_HOSTS="$DS1 $DS2 $DS3"  # IP/DNS names of all ZooKeeper nodes.
```
 
```
# Cassandra information.  
CASS_CLUSTERNAME=Apigee    # Default name is Apigee.
```
 
```
# Space-separated IP/DNS names of the Cassandra hosts (previously defined)  
CASS_HOSTS="$DS1:1,1 $DS2:1,1 $DS3:1,1"
```
 
```
# Set to enable Cassandra authentication.  
# CASS_AUTH=y    # The default value is n.  
# Cassandra uname/pword required if you enabled Cassandra authentication.  
# CASS_USERNAME=  
# CASS_PASSWORD=
```
      

```
# Postgres username and password as set when you installed Edge.  
# Default is apigee:postgres.  
PG_USER=apigee  
PG_PWD=postgres
```
 
```
# Use to enable Postgres master-standby replication  
# when you have multiple Postgres nodes.  
# PG_MASTER=IPorDNSofNewMaster  
# PG_STANDBY=IPorDNSofOldMaster
```
       
```
# SMTP information.  
SKIP_SMTP=n       # Skip now and configure later by specifying "y".  
SMTPHOST=smtp.gmail.com  
SMTPUSER=magnon2k@gmail.com  
SMTPPASSWORD=yourEmailPassword  
SMTPSSL=y  
SMTPPORT=465      # If no SSL, use a different port, such as 25.  
SMTPMAILFROM="BliexSoft \<noreply@bliex.com\>"
```