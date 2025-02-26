---
tags:
  - Backup
  - Mysql
  - Server
  - Sharejob
  - db
Created: Invalid date
Updated: Invalid date
---
crontabhttp://webdir.tistory.com/174mysqldump -u root -p sharejob > sharejob_dev_160329.sql0 4 * * 1-7 /srv/www/api.sharejob.me/scripts/db_live_data_export_to_dev_file.sh0 5 * * 1-7 /srv/www/api.sharejob.me/scripts/db_live_data_import_to_dev_backup.sh