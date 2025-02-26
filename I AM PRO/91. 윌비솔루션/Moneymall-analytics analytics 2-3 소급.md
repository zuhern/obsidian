---
Created: Invalid date
Updated: Invalid date
---
**자바 소스**

moneymall-src/batch/src/main/java/com/shinsegae/moneymall/mr/analytics/AnalyticsIf2_3EveryClickEvent.java

**명령어**

git pull

mvn -e -DskipTests clean install assembly:single -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_3EveryClickEventTestSkip test -P prod -nsu

/data01/

moneymall

-shell/merge_hadoop_directory.sh /

moneymall

/analytics/analytics-if-2-3-every-click-event/

temp

/data01/

temp

every_click_item_view.txt

mysqlimport -L --host=10.203.5.47 --user=bigdata --password=bigdata --fields-terminated-by='\t' --lines-terminated-by='\n' DW /data01/temp/every_click_item_view.txt