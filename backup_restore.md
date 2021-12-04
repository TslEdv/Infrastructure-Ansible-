MySQL restoration:

Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Go to TslEdv2 (or any other VM that is MASTER)
Enter super user mode:

    sudo su

Change to user called backup

    sudo -u backup -s

Get restore from other server

    duplicity --no-encryption restore rsync://TslEdv@backup//home/TslEdv/mysql /home/backup/restore/

Exit from backup user

    exit

Restore MySQL DB with the newly acquired file

    mysql agama < /home/backup/restore/agama.sql


InfluxDB restoration:

Install and configure infrastructure with Ansible:

    ansible-playbook infra.yaml

Go to TslEdv2 (or any other VM that is MASTER)
Enter super user mode:

    sudo su

Stop telegraf service:

    service telegraf stop

Delete existing telegraf database:

    influx -execute 'DROP DATABASE telegraf'

Change to user called backup

    sudo -u backup -s

Get restore from other server

    duplicity --no-encryption restore rsync://TslEdv@backup//home/TslEdv/influxdb /home/backup/influxdb/

Exit from backup user

    exit

Restore InfluxDB with newly acquired file:

    influxd restore -portable -database telegraf /home/backup/influxdb

Rerun ansible-playbook:

    ansible-playbook infra.yaml

