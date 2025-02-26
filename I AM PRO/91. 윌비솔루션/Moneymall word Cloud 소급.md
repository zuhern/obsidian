---
Created: Invalid date
Updated: Invalid date
---
2014-08-02 word cloud 소급

1)

TestLoadToTableCustomerSearchAnyDay 로 검색해서

spring-job-runner-context-test.xml

안에 있는 날짜를 일괄적으로 수정하기 ex)<value]]  
2014-08-27</value]]  

2) 서버에서

하루하루치

mvn -e -Dtest=TestLoadToTableCustomerSearchAnyDayTestSkip test -P prod -nsu

mvn -e -Dtest=TestLoadToTableCustomerSearchDayGroupAnyDayTestSkip test -P prod -nsu

3)

30일치씩 묶어서

mvn -e -Dtest=TestWordCloudSearchKeywordWordDailyUnionAnyDayTestSkip test -P prod -nsu

mvn -e -Dtest=TestWordCloudSearchKeywordWordMonthTopCountAnyDayTestSkip test -P prod -nsu

mvn -e -Dtest=TestWordCloudSearchKeywordWordDailyJoinCountAnyDayTestSkip test -P prod -nsu

4)

select * from SEARCH_WORD_CLOUD where etldt = ‘20140828'

20140827 데이터면 etldt가 원하는 날짜 데이터를 만드는 날짜인 20140828로 되어있으므로

유의하여 데이터를 지운다.

5)  
/  
moneymall/workspace/customer-search-daily-result 를  
/  
moneymall/workspace-backup/2014-08-05/customer-search-daily-result 로 바꿔서

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=exportWordCloudDailyJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

6)

/moneymall/workspace-backup/2014-08-05/customer-search-daily-result 를

/moneymall/workspace/customer-search-daily-result 로 다시 원복

=============================================================================

git pull

mvn -e -DskipTests clean install assembly:single -P prod -nsu

mvn -e -Dtest=TestLoadToTableCustomerSearchAnyDayTestSkip test -P prod -nsu

mvn -e -Dtest=TestLoadToTableCustomerSearchDayGroupAnyDayTestSkip test -P prod -nsu

git pull

mvn -e -DskipTests clean install assembly:single -P prod -nsu

mvn -e -Dtest=TestWordCloudSearchKeywordWordDailyUnionAnyDayTestSkip test -P prod -nsu

mvn -e -Dtest=TestWordCloudSearchKeywordWordMonthTopCountAnyDayTestSkip test -P prod -nsu

mvn -e -Dtest=TestWordCloudSearchKeywordWordDailyJoinCountAnyDayTestSkip test -P prod -nsu

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=exportWordCloudDailyJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

=============================================================================

sqoop 소스

=============================================================================

export  
-D  
sqoop.export.records.per.statement=100000  
-D  
sqoop.export.statements.per.transaction=1  
--batch  
--num-mappers  
1  
--driver  
org.mariadb.jdbc.Driver  
--connect  
jdbc:mariadb://10.203.5.27:3306/CEO_REPORT  
--table  
SEARCH_WORD_CLOUD  
--export-dir  
/moneymall/workspace/customer-search-daily-result  
--username  
root  
--password  
root  
--fields-terminated-by  
\t