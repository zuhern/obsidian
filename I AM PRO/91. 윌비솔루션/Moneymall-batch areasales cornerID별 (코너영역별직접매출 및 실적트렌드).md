---
Created: Invalid date
Updated: Invalid date
---
1)

job : delete-pdw-cornerid-info.job

dependencies : sqoop-export-ctg-cornr-cnt

command : /data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/workspace/pdw-cornerid-info

대상 폴더 : /moneymall/workspace/pdw-cornerid-info

2) 코너ID, 카테고리ID

job : sqoop-import-pdw-cornerid-info.job

Runner : importPdwCornerIdInfoJobRunner

sqoop : META-INF/sqoop/sqoop-import-cornerid/lib/import.txt

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importPdwCornerIdInfoJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

3)

job : delete-pdw-amt-by-cornerid.job

command : /data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/workspace/pdw-amt-by-cornerid

대상 폴더 : /moneymall/workspace/pdw-amt-by-cornerid

4)

PDW에서 매출, 건수, 이익 가지고 오는 쿼리 (코너ID, 카테고리ID가 있는 것만 계산 / 템플릿ID는 bigdata팀에서 전달해 주지 않기 때문에 없는 상태)

job : sqoop-import-pdw-amt-by-cornerid.job

Runner : importPdwAmtByCornerIdJobRunner

sqoop : META-INF/sqoop/sqoop-import-amt-by-cornerid/lib/import.txt

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importPdwAmtByCornerIdJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

5)

java : EveryClickVisitCntByCornerId.java

Runner : everyClickVisitCntByCornerIdJobRunner

test : EveryClickVisitCntByCornerIdTestSkip

job : lt-table-every-click-visit-cnt-by-cornerid.job

mvn -e -Dtest=EveryClickVisitCntByCornerIdTestSkip test -P prod -nsu

6)

job : sqoop-export-result-of-cornerid.job

Runner : exportLtTableResultOfCorneridJobRunner

sqoop : META-INF/sqoop/sqoop-export-result-of-cornerid/lib/export.txt

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=exportLtTableResultOfCorneridJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

-- 소스 받고 빌드

git pull

mvn -e -DskipTests clean install assembly:single -P prod -nsu

-- 매출 DB에서 HDFS로

/data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/workspace/pdw-amt-by-cornerid

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importPdwAmtByCornerIdJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

-- 하둡

--mvn -e -Dtest=EveryClickVisitCntByCornerIdTestSkip test -P prod -nsu

mvn -e -DconfPath=/META-INF/spring/visualization/*-context.xml -DbeanName=everyClickVisitCntByCornerIdJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

-- DB로 데이터 밀어넣기

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=exportLtTableResultOfCorneridJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

###################################################################################

select * from RESULT_OF_AREASALES order by dt desc

delete from RESULT_OF_AREASALES where DT = '20140715'