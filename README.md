# ansible-backupninja
                                          |\_
                 B A C K U P N I N J A   /()/
                                         `\|

This role install backupninja and can install backup scripts for gcloud.

## actions before of after gsutil backup

All backups instructions are defined in `/etc/backup.d`. gcloud is `50_` prefixed. Actions will be performed in alphabetical order. If you want a mysql dump before gcloud rsync you must create a file like `40_dump.mysql`.

If you need to perfom actions after gsutil (like a backup test), just need create a file like `60_call-jenkins-test-backup.sh` if it's a shell script.

For test you can set `backupninja_reportsuccess` to `yes` in inventory. All backups will trigger an email.

## gcloud backup

To use gcloud backup :
  - `ansible-gcloud` must be deploy before ( https://github.com/leucos/ansible-gcloud )
  - `gcloud_{daily,hourly}_backup` must be `TRUE`
  - `gsutil` must be properly configured
  - `source and destination` must me defined like this :

```
gcloud_{daily,hourly}_sync:
  - source: "/etc"
    destination: "my_bucket/etc/"
  - source: "/home"
    destination: "my_bocket/home/"
```
