Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Restore MySQL data from the backup:

  On the managed host with mysql server (check [hosts](/hosts) file to see which host located in [db_servers] group) run this commands:
    # to restore the MySQL backup files from the remote server to the local directory /home/backup/restore/mysql
    `sudo -u backup duplicity --no-encryption restore rsync://manuniia@backup/mysql /home/backup/restore/mysql`
    # to import the SQL data from the agama.sql file into the agama database on the MySQL server
    `mysql agama < /home/backup/mysql/agama.sql`

<add a few words here how the result of backup restore can be checked>