---
Created: Invalid date
Updated: Invalid date
---
// 데이터 소급할 때 수정할 곳 20140804

1) 날짜 바꾸는 곳  
analytics-If-2_4-join  
batch/src/main/resources/META-INF/sqoop/sqoop-import-result-of-channel/lib/ckwhere/import.txt  
EveryClickVisitCntByCkWhere  
batch/src/main/resources/META-INF/sqoop/sqoop-import-ctg-cornr-cnt/lib/import.txt  
batch/src/main/resources/META-INF/sqoop/sqoop-import-amt-by-cornerid/lib/import.txt  
CornrSales  

2) job 임시로 바꾸기

delete-temp-result-for-ckwhere-folder.job

dependencies=hive-ld-data-analytics-if-2-4

3) 소급하기 - sh 파일이여서 무조건 어제 날짜로 돌기 때문

mvn -e -Dtest=AnalyticsIf2_4JoinTestSkip test -P prod -nsu  
hadoop fs -cp /moneymall/analytics/if2-4/analytics-if-2-4/2014-08-01 /moneymall/analytics/hive-load-data-temp  

/data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/analytics/hive-load-data-temp/' into table analytics_if_2_4"

위 에러나면

/data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/analytics/hive-load-data-temp/날짜' into table analytics_if_2_4"

한 후 아즈카반에서 project 돌리기

- delete-temp-result-for-ckwhere-folder 에서 시작하는 부분을 따로 떼어서 실행

4) 확인

hive ) select * from analytics_if_2_4 where date="2014-08-01";

maridDB )

select * from RESULT_OF_CHANNEL where dt='20140801';

select * from CTG_CORNR_CNT where etldt='20140801';

select * from RESULT_OF_CORNRSALES where dt='20140801';

---참조 ---

명령어 :

analytics-If-2_4-join mvn -e -Dtest=AnalyticsIf2_4JoinTestSkip test -P prod -nsu  
move-hd-for-hive-analytics-if-2-4 hadoop fs -cp /moneymall/analytics/if2-4/analytics-if-2-4/2014-08-01 /moneymall/analytics/hive-load-data-temp  
hive-ld-data-analytics-if-2-4 /data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/analytics/hive-load-data-temp/' into table analytics_if_2_4"  

delete-temp-result-for-ckwhere-folder /data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/visualization/temp-result-for-ckwhere  
sqoop-import-result-of-channel mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importResultOfChannelFromPdwJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu  

lt-table-every-click-visit-cnt-by-ckwhere mvn -e -Dtest=EveryClickVisitCntByCkWhereTestSkip test -P prod -nsu  
sqoop-export-result-of-channel mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=exportResultOfChannelJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu  

delete-temp-ctg-cornr-count /data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/visualization/temp-ctg-cornr-count  
sqoop-import-pdw-ctg-cornr mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importCtgCornrDataFromPdwJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu  

sqoop-export-ctg-cornr-cnt  
delete-cornr-list-for-cornr-sales  
sqoop-import-cornr-list-for-cornr-sales  
delete-pdw-amt-by-cornerid  
sqoop-import-pdw-amt-by-cornerid mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importPdwAmtByCornerIdJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu  

================================================================================================================================================================================

mvn -e -Dtest=AnalyticsIf2_4JoinTestSkip test -P prod -nsu  
hadoop fs -cp /moneymall/analytics/if2-4/analytics-if-2-4/2014-08-01 /moneymall/analytics/hive-load-data-temp  

/data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/analytics/hive-load-data-temp/' into table analytics_if_2_4"  
/data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/visualization/temp-result-for-ckwhere  
mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importResultOfChannelFromPdwJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu  
mvn -e -Dtest=EveryClickVisitCntByCkWhereTestSkip test -P prod -nsu  
mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=exportResultOfChannelJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu  
/data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/visualization/temp-ctg-cornr-count  
mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importCtgCornrDataFromPdwJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu