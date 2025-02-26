---
Created: Invalid date
Updated: Invalid date
---
local에서 data파일 생성

scp data moneymall@10.203.5.31:~/

hadoop fs -mkdir /moneymall/temp/temp-anal

hadoop fs -put ~/data /moneymall/temp/temp-anal

/data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/temp/temp-anal/data' into table analytics_if_4_1"