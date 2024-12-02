Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Restore MySQL data from the backup:

  On the managed host with mysql server (check [hosts](/hosts) file to see which host located in [db_servers] group) run this commands:
    # to restore the MySQL backup files from the remote server to the local directory /home/backup/restore/mysql
    `sudo -u backup duplicity --no-encryption restore rsync://manuniia@backup/mysql /home/backup/restore/mysql`
    # to import the SQL data from the agama.sql file into the agama database on the MySQL server
    `mysql agama < /home/backup/mysql/agama.sql`

Check the result of MySQL data restore:
  Open http://193.40.156.67/students/manuniia.html for Public HA url on vm-1
    

Restore Influxdb data from the backup:

  On the managed host with mysql server (check [hosts](/hosts) file to see which host located in [influxdb] group) run this commands:
    # to restore the Influxdb backup files from the remote server to the local directory /home/backup/restore/influxdb
    `sudo -u backup duplicity --no-encryption restore rsync://manuniia@backup/influxdb /home/backup/restore/influxdb`
    # stop telegraf service to prevent it of creatinf table
    `service telegraf stop`
    # delete existing database telegraf
    `influx -execute 'DROP DATABASE telegraf`
    # to import the telegraf data into the influxdb database
    `influxd restore -portable -db telegraf /home/backup/restore/influxdb`

Check the result of Influxdb data restore:
  Open Grafana Telagraf dashboard to see restored results
