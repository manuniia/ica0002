# Backup SLA

## Coverage

We back up services that satisfy at least one of these criteria:
 - are primary source of truth for particular data
 - contain customer and/or client data
 - are not feasible (or very costly) to restore by other means

Services that are backed up:
 - MySQL
 - InfluxDB
 - Ansible Git Repository


## Schedule

MySQL backups are created every day; it takes up to 20 mins to create and store the backup.

InfluxDB backups are created every day; it takes up to 20 mins to create and store the backup.

Ansible Git Repository backups are created every day; it takes up to 20 mins to create and store the backup.

All backups are started automatically by cron jobs managed through Ansible.

Backup RPO (recovery point objective) is:
 - 8 hours for MySQL
 - 8 hours for InfluxDB
 - 2 hours for Ansible Git Repository


## Storage

MySQL and InfluxDB backups are uploaded to the backup server.

Ansible Git Repository is mirrored to the internal Git server.

Backup data from both servers will be synchronized to encrypted AWS S3 bucket in future (work in progress).


## Retention

MySQL backups are stored for 30 days; 30 versions (recovery points) are available to restore.

InfluxDB backups are stored for 30 days; 30 versions are available to restore.

Ansible Git Repository backups are stored indefinitely; historical versions are available to restore via the Git commit history.


## Usability checks

MySQL backups are verified every week by restoring a test database.

InfluxDB backups are verified every week by restoring to a test environment.

Ansible Git Repository backups are verified every week by checking the mirror for consistency with the live repository.


## Restore process

Service is recovered from the backup in case of an incident, and when service cannot be restored in any other way.

RTO (recovery time objective) is:
 - 2 hours for MySQL
 - 2 hours for InfluxDB
 - 1 hour for Ansible Git Repository

Detailed backup restore procedure is documented in the [backup_restore.md](./backup_restore.md).