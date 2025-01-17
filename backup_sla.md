# [Backup coverage]

We back up services that satisfy at least one of these criteria:

1.Are primary source of truth for particular data
2.Contain customer and/or client data
3.Are not feasible (or very costly) to restore by other means

Services that are backed up:

- MySQL
- InfluxDB
- group_vars all.yaml
 

# [ Storage ]

    MySQL and InfluxDB backups are uploaded to the backup server.

    all.yaml is mirrored to the internal Git server.

    Backup data from both servers will be synchronized to encrypted AWS S3 bucket in future (work in progress).

# [ Schedule ]

    Full MySQL/Influx backup - performed every Sunday at 12.04 
    Incremental MySQL/Influx backup - (Monday -> Saturday) 12.04
    15-25 minutes - tume required to create and store the backup
    All backups are started automatically by cron.
    RPO is set to 24 hours.

# [ Retention ]

    Full backup - kept for 40 days. Store 5 versions.
    Incremental backup - kept for 40 days. Store 40 versions.
    All the other important data including tasks/structure/configurations has the backup in both internal and remote git repository.


# [ Usability checks ]

    Usability of backup is checked by simulating a recovery scenario by temporarily restoring the backup to a non-production environment once a month.

# [ Restore process ]

    RTO (recovery time objective):
    30 minutes for git repository
    2 hours for MySQL database
    2 hours for InfluxDB database