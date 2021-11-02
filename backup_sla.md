Backup coverage - 

We backup: MySQL, InfluxDB and Ansible repository

From MySQL we backup the stored data.
From InfluxDb we backup the stored data.
Ansible repository is mirrored on another server, we backup the whole repository and it's history.

RPO - 

We create incremential backups every night at 1 am UTC.
We create full backups every sunday at 1 am UTC.
Acceptable data loss - 12h after the last backup.

Versioning and retention - 

We keep our backups for 30 days and thus we make 30 versions.
Retention is 30 days.

Usability checks -

The senior infrastructure engineer verifies that the backup is working every first Monday of the month.
Senior builds the infrastructure using backup ansible and add the required MySQL and InfluxDB.

Restoration criteria -

If the infrastructure becomes unavailable and the infrastructure team as a whole cannot figure out another way of solving the problem
within 5 hours.

RTO -

4 hours
