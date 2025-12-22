khugepageds kerberods
    
sudo amazon-linux-extras install epel  
sudo yum install s3fs-fuse
    
sudo /usr/local/bin/s3fs bx-intra-backup /app/s3-bx-intra-backup -o passwd_file=/etc/passwd_s3-bx-intra-backup-user  
sudo s3fs bx-intra-backup /app/s3-bx-intra-backup -o passwd_file=/etc/passwd_s3-bx-intra-backup-user
   

sudo fusermount -u /app/s3-bx-intra-backup
    
$ crontab -l
 
# remove backup - every day 4AM KST  
0 19 * * * /home/ec2-user/cron-script/removeBackup.sh &\>\> /home/ec2-user/cron-script/removeBackup-`date +\%Y\%m\%d`.log
 
# check live confluence - 5 minutes  
#*/5 * * * * /home/ec2-user/cron-script/checkConfluenceLive.sh &\>\> /home/ec2-user/cron-script/checkConfluenceLive-`date +\%Y\%m\%d`.log
 
# check response status code - 5 minutes  
#*/30 * * * * /home/ec2-user/cron-script/check_resp_status_code.sh
          
$ cat /etc/init.d/confluence  
#!/bin/bash
 
# Confluence Linux service controller script  
cd "/app/confluence/home/bin"
 
case "$1" in  
start)  
./start-confluence.sh  
;;  
stop)  
./stop-confluence.sh  
;;  
restart)  
./stop-confluence.sh  
./start-confluence.sh  
;;  
*)  
echo "Usage: $0 {start|stop|restart}"  
exit 1  
;;  
esac
   

AAABQg0ODAoPeNptkMtqwzAQRff6CkE37cJBceO2CQja2C64OHaonZJFN4o6SQSyHPQIyd9XfhRKK  
Wg2unPn3Jmb2gF+hR0mISazRThdkCccVzUOyfQBFa7ZgS73GwPa0IigBAzX4mRFq2jcqr10oDjg2  
wr0GfQdjgjuez8XOG6bBjQXTOJccFAGUKyBddaEWaAdICChf8hPsozbgjVAl606GKZwfGwF4h4x8  
Yo4A7XawfBRWaYtaLpnshs6mNMVE5LynXmGi7JuwtsGpWcmXU8ce3v7mKa+nqAnxuVqlb7H2UuO5  
CB9+A06U4j8UGVBMb9kejkJff2J/jhGL/WBKWEGSNqRsVB8goaDZAldvmXboJhHZZDX0X2wSbcbV  
KUF9RXM5vNoFhI0JvLdeZb8I/xCOyVFIyx8obXT/MgM/D3mNwSDmXgwLAIUDpfStORNB8uRShp9+  
DHtkI10XVECFFXeCVd2FfJ735E2NEwML54K2tXjX02g0
   

jdbc:mysql://localhost/confluence?sessionVariables=storage_engine%3DInnoDB&useUnicode=true&characterEncoding=utf8  
cnfldbuser  
cnfldbuser!
    
\<property name="confluence.setup.server.id"\>BG08-BY6G-QTJR-3J3K\</property\>
   

mysqldump -h cnfldb2.cmaeupu4u0sr.ap-northeast-2.rds.amazonaws.com -u cnfldbuser -p --databases cnfldb2 \> bliex_wiki_db_backup_20190415.sql