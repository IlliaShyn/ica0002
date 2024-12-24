# [Backup coverage]

We back up services that satisfy at least one of these criteria:

1.Are primary source of truth for particular data
2.Contain customer and/or client data
3.Are not feasible (or very costly) to restore by other means

Services that are backed up:

- MySQL
- InfluxDB
- group_vars all.yaml


# [ Schedule ]

    Full backups are performed weekly. Incremental and Differential backups performed every day.
    Full backup - performed every Sunday at 00:20 - kept for 30 days. Store 4 versions.
    Incremental backup - (Monday -> Saturday) 00:25 - kept for 30 days. Store 30 versions. RPO - 24 hours. All backups are started automatically by cron.
 

# [ Storage ]

    MySQL and InfluxDB backups are uploaded to the backup server.

    all.yaml is mirrored to the internal Git server.

    Backup data from both servers will be synchronized to encrypted AWS S3 bucket in future (work in progress).



# [ Retention ]

    Full backup - performed every Sunday at 12.04 - kept for 40 days. Store 4 versions.
    Incremental backup - (Monday -> Saturday) 12.04 - kept for 40 days. Store 30 versions. 


# [ Usability checks ]

    Usability of backup is checked by simulating a recovery scenario by temporarily restoring the backup to a non-production environment once a month.

# [ Restore process ]

    RTO (recovery time objective) is 3 hours