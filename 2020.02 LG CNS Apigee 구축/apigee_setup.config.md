```
### [https://docs.apigee.com/private-cloud/v4.19.06/edge-configuration-file-reference](https://docs.apigee.com/private-cloud/v4.19.06/edge-configuration-file-reference)
```
 
```
# IP address or DNS name of nodes.  
DS1=10.1.100.13  
DS2=10.1.100.26  
DS3=10.1.100.27  
DS4=10.1.100.43  
DS5=10.1.100.46
```
 
```
RMP1=10.1.100.6  
RMP2=10.1.100.52
```
 
```
SAX1=10.1.100.23  
SAX2=10.1.100.42
```
 
```
MS1=10.1.100.36
```
 
```
DP1=10.1.100.55
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
ADMIN_EMAIL=lgstation.root@gmail.com  
APIGEE_ADMINPW="Bldcnt2020&*()"
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
```
    
```
APIGEE_LDAPPW="Bldcnt2020&*()"
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
ZK_HOSTS="$DS1 $DS2 $DS3 $DS4 $DS5"         # IP/DNS names of all ZooKeeper nodes.  
ZK_CLIENT_HOSTS="$DS1 $DS2 $DS3 $DS4 $DS5"  # IP/DNS names of all ZooKeeper nodes.
```
    
```
# Cassandra information.  
CASS_CLUSTERNAME=Apigee    # Default name is Apigee.
```
    
```
# Space-separated IP/DNS names of the Cassandra hosts (previously defined)  
CASS_HOSTS="$DS1:1,1 $DS2:1,1 $DS3:1,1 $DS4:1,2 $DS5:1,2"
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
PG_PWD="Bldcnt2020&*()"
```
    
```
# Use to enable Postgres master-standby replication  
# when you have multiple Postgres nodes.  
PG_MASTER=$SAX1  
PG_STANDBY=$SAX2
```
    
```
# SMTP information.  
SKIP_SMTP=n                  # Skip now and configure later by specifying "y".  
SMTPHOST=smtp.gmail.com  
SMTPUSER=lgstation.root@gmail.com  
SMTPPASSWORD="Bldcnt2020&*()"  
SMTPSSL=y  
SMTPPORT=465                 # If no SSL, use a different port, such as 25  
SMTPMAILFROM="lgstation.root@gmail.com"
```