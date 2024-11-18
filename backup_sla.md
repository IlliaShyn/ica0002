# RESTORING MYSQL DATABASE FROM A BACKUP


1.Play ansible-playbook to built the infrastructure


    ansible-playbook infra.yaml


2.Find out which hosts are in 'db_servers' group and ssh connect to one.


Connection via ssh:
   
    ssh ubuntu@<public ip address> -p <port>  or  ssh -p <port> ubuntu@193.40.156.67 


3.Downloading of files from backup server:
   
    sudo -u backup duplicity --no-encryption restore rsync://IlliaShyn@backup.agamais.ttu/mysql /home/backup/restore/mysql


4.Switch to the root user:


    sudo su - 


5.Restore data from the backup:


    mysql agama < /home/backup/mysql/agama.sql




# INFLUXDB PART


1.Play ansible-playbook to built the infrastructure


    ansible-playbook infra.yaml


2.Find out which hosts are in 'influxdb' group and ssh connect to one.


Connection via ssh:
   
    ssh ubuntu@<public ip address> -p <port>  or  ssh -p <port> ubuntu@193.40.156.67 


3.Downloading of files from backup server:
   
    sudo -u backup duplicity --no-encryption restore rsync://IlliaShyn@backup.agamais.ttu/influxdb /home/backup/restore/influxdb


Stop Telegraf service:


    sudo service telegraf stop


Delete database:


    influx -execute 'DROP DATABASE telegraf'


Restore Telegraf data from the backup:


    sudo influxd restore -portable -database telegraf /home/backup/restore/influxdb


To start Telegraf run playbook:


    ansible-playbook infra.yaml

