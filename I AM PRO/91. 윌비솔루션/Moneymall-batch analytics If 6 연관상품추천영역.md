---
tags:
  - Hive
Created: Invalid date
Updated: Invalid date
---
analytics6

### 하이브 Hive로 바로 데이터 넣기

if(templId.equals("F000000000")||templId.equals("S000000000")||templId.equals("T000000000"))) {

importProductDetailResultAgrtDwJobRunner

importProductDetailResultAgrtDispCtgJobRunner

productDetailResultAgrtJobRunner

productDetailResultAgrtJoinJobRunner

소급명령어

/data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/adhoc/product-detail-result-agrt-dw

git pull

mvn -e -DskipTests clean install assembly:single -P prod -nsu

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importProductDetailResultAgrtDwJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

mvn -e -Dtest=ProductDetailResultAgrtTestSkip test -P prod -nsu

mvn -e -Dtest=ProductDetailResultAgrtJoinTestSkip test -P prod -nsu

/data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/adhoc/product-detail-result-agrt-final/' into table recommend_result"

명령어

/data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/adhoc/product-detail-result-agrt-dw

/data01/moneymall-shell/delete_hadoop_directory.sh /moneymall/adhoc/product-detail-result-agrt-disp-ctg

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importProductDetailResultAgrtDwJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

mvn -e -DconfPath=/META-INF/spring/import-export-db/*-test.xml -DbeanName=importProductDetailResultAgrtDispCtgJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

mvn -e -Dtest=ProductDetailResultAgrtTestSkip test -P prod -nsu

mvn -e -Dtest=ProductDetailResultAgrtJoinTestSkip test -P prod -nsu

/data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/adhoc/product-detail-result-agrt-final/' into table recommend_result"

delete-product-detail-result-agrt.job

delete-product-detail-result-agrt-join.job

sqoop-import-product-detail-result-agrt.job importProductDetailResultAgrtDwJobRunner sqoop-import-product-detail-result-agrt-join.job importProductDetailResultAgrtDispCtgJobRunner

analytics-if-6-product-detail-result-agrt.job

analytics-if-6-delete-product-detail-result-agrt-join.job

analytics-if-6-product-detail-result-agrt-to-hive.job

테이블 생성시 하둡경로는 없게한다.

CREATE EXTERNAL TABLE RECOMMEND_RESULT(

siteNo STRING

,templId STRING

,dispCtgLclsNm STRING

,dispCtgLclsId STRING

,count BIGINT

,vatExclOrordCnt BIGINT

,vatExclOrordamtSum BIGINT

,currDate STRING

)ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' ;

데이터 밀어넣는 명령어

/data01/hive/hive-0.11.0/bin/hive -h 10.203.5.21 -p 10000 -e "load data inpath '/moneymall/adhoc/product-detail-result-agrt-final/' into table recommend_result"