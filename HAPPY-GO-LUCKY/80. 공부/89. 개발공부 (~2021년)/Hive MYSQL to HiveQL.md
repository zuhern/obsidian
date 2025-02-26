---
Created: Invalid date
Updated: Invalid date
---
예제소스 : [MYSQLtoHiveQL.zip](http://wiki.moneymall.ssgadm.com:8010/download/attachments/1836918/MYSQLtoHiveQL.zip?version=1&modificationDate=1410744891000&api=v2) (기존MYSQL쿼리파일, Shell파일, 스쿱파일, 하이브쿼리 파일

> 아즈카반에서 Hive 호출 순서   
> 아즈카반job에서 shell 호출 or (테스트할 때) 바로 shell 호출shel 에서 sqoop 호출하여 DB데이터를 Hadoop으로 옮김  
> 스쿱 파일 호출형식sqoop --options-file 스쿱파일경로예시sqoop --options-file /data01/research-shell/sqoop/proc_input_ord.txtshell 에서 Hive쿼리 호출직접 쿼리 호출형식hive -e "쿼리";예시hive -e "DROP TABLE IF EXISTS RESEARCH.ORD_ITEM";SQL파일 호출형식hive -f "하이브쿼리파일(.sql or .hql) 파일경로";예시hive -f "/data01/research-shell/sql/proc_input_ord.sql";set hive.auto.convert.join=false; sql파일 맨 앞 줄에 안 적으면 조인이 안되는 경우가 있음.MYSQL 에서 HiveQL로 변경  
>  DROP, CREATE, JOIN, INSERTMYSQLHIVEQL형식CREATE : 1.하둡경로와 연동2. EXTERNAL TABLE은 TABLE DROP하였을 때 하둡상 데이터가 남아 있음그 후 다시 테이블을 생성하면 이전 데이터로 SELECT됨.EXTERNAL을 적지 않으면 TABLE DROP하였을 때 하둡데이터도 삭제됨3. 하둡경로 삭제형식하둡경로삭제쉘.sh 하둡경로;예시/data01/moneymall-shell/delete_hadoop_directory.sh /user/hive/warehouse/research_ord_item;/data01/moneymall-shell/delete_hadoop_directory.sh 소스#! /bin/shHADOOP_DIRECTORY="$1"hadoop fs -test -d $HADOOP_DIRECTORYCHECKDIR=$?  
> echo "result=$CHECKDIR"if [ $CHECKDIR -eq 0 ]; then  
> hadoop fs -rmr $HADOOP_DIRECTORY  
> echo "delete complete!"  
> else  
> echo "directory already deleted!!"  
> fiDROP TABLE IF EXISTS 테이블명;  
> CREATE EXTERNAL TABLE RESEARCH.ORD_ITEM(  
> 컬럼명1 STRING,  
> 컬럼명2 INT,  
> 컬럼명3 BIGINT,  
> 컬럼명4 DECIMAL,  
> ) ROW FORMAT DELIMITED FIELDS TERMINATED BY '하둡컬럼구분자'  
> LINES TERMINATED BY '하둡로우구분자'  
> STORED AS TEXTFILE LOCATION '하둡 내 데이터경로'";  
> CREATE TABLE 테이블명1 AS  
> SELECT 컬럼명1, 컬럼명2  
> FROM (  
> SELECT A1.컬럼명1, A1.컬럼명3  
> FROM 테이블명  
> ) A1  
> LEFT OUTER JOIN 테이블명2 A2 ON A1.컬럼명1 = A2.컬럼명1;  
> INSERT INTO 테이블명1 (컬럼명3, 컬럼명4)  
> SELECT 컬럼명1, 컬럼명2  
> FROM 테이블명2;  
> INSERT OVERWRITE TABLE 테이블명1  
> SELECT 컬럼명1, 컬럼명2  
> FROM 테이블명2;  
> 예시DROP TABLE IF EXISTS RESEARCH.temp_ord_item;  
> CREATE TABLE RESEARCH.temp_ord_item AS  
> SELECT t1.ord_no, t1.mbr_id, t1.item_id, t2.std_ctg_depth_id, t1.brand_id  
> FROM (  
> SELECT ord_no, mbr_id, item_id, std_ctg_id, brand_id  
> FROM DW.ORD_ITEM USE INDEX (ord_dt)  
> WHERE ord_dt >= concat(use_yy,'-',use_mm,'-',01)  
> AND ord_dt < concat(yy,'-',mm,'-',01)  
> AND orord_no=ord_no  
> ) t1  
> LEFT JOIN RESEARCH.std_ctg_depth t2 ON t1.std_ctg_id=t2.std_ctg_dcls_id;  
> CREATE INDEX ord_no ON RESEARCH.temp_ord_item(ord_no);  
> CREATE INDEX mbr_id ON RESEARCH.temp_ord_item(mbr_id);  
> CREATE INDEX item_id ON RESEARCH.temp_ord_item(item_id);  
> CREATE INDEX std_ctg_depth_id ON RESEARCH.temp_ord_item(std_ctg_depth_id);  
> CREATE INDEX brand_id ON RESEARCH.temp_ord_item(brand_id);  
> DROP TABLE IF EXISTS RESEARCH.temp_ord_item;  
> CREATE EXTERNAL TABLE RESEARCH.ORD_ITEM(  
> ord_no STRING, site_no STRING,  
> mbr_id STRING, item_id STRING,  
> std_ctg_id STRING, brand_id STRING  
> ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ','  
> LINES TERMINATED BY '\n'  
> STORED AS TEXTFILE LOCATION '/user/hive/warehouse/research_ord_item'";  
> CREATE TABLE RESEARCH.temp_ord_item AS  
> SELECT t1.ord_no, t1.mbr_id,  
> t1.item_id, t2.std_ctg_depth_id, t1.brand_id  
> FROM (  
> SELECT ord_no, mbr_id, item_id, std_ctg_id, brand_id  
> FROM RESEARCH.ORD_ITEM  
> ) t1  
> LEFT OUTER JOIN RESEARCH.std_ctg_depth t2 ON t1.std_ctg_id=t2.std_ctg_dcls_id;  
> INSERT INTO RESEARCH.temp_mbr_shopp_score_potential (shopp_id, mbr_id, score, last_id)  
> SELECT t2.shopp_id, t1.mbr_id,  
> cast(sum(t1.std_ctg_score*t2.weight) as DECIMAL(25,3)) AS score,  
> MAX(t1.last_id) AS last_id  
> FROM RESEARCH.tb_mbr_std_ctg_score t1 USE INDEX (last_id)  
> LEFT JOIN RESEARCH.temp_shopp_std_ctg_depth_score t2  
> ON t1.site_name=t2.site_name  
> AND t1.std_ctg_depth_id=t2.std_ctg_depth_id  
> WHERE t1.last_id=',n,' AND t2.shopp_id IS NOT NULL  
> AND t2.weight IS NOT NULL  
> AND t1.std_ctg_score IS NOT NULL  
> GROUP BY t1.site_name, t2.shopp_id, t1.mbr_id;  
> INSERT OVERWRITE TABLE RESEARCH.tb_mbr_shopp_score_potential  
> SELECT t2.shopp_id, t1.mbr_id,  
> cast(sum(t1.std_ctg_score*t2.weight) as DECIMAL) AS score  
> FROM RESEARCH.tb_mbr_std_ctg_score t1  
> LEFT OUTER JOIN RESEARCH.temp_shopp_std_ctg_depth_score t2  
> ON t1.std_ctg_depth_id=t2.std_ctg_depth_id  
> WHERE t2.shopp_id IS NOT NULL  
> AND t2.weight IS NOT NULL  
> AND t1.std_ctg_score IS NOT NULL  
> GROUP BY t2.shopp_id, t1.mbr_id;  
> Azkaban Job으로 호출하는 방법 및 전체 흐름  
> job 파일 (analytics5_04_proc_input_clck.job)형식type=타입  command=쉘경로.sh dependencies=바로앞 job명예시type=commandcommand=/data01/research-shell/proc_input_clck.sh dependencies=analytics5_04_java_input_clck쉘 파일형식#! /bin/sh  
> # TABLE 삭제 생성  
> echo "delete hdfs path!!"  
> 하둡경로삭제쉘.sh 하둡경로;  
> echo "drop hive table"  
> hive -e "DROP TABLE IF 테이블명1";  
> echo "sqoop start!"  
> sqoop --options-file 스쿱파일.txt  
> echo "테이블 CREATE"  
> hive -e "테이블 CREATE";  
> hive -f "하이브쿼리파일.sql";  
> 예시#! /bin/sh  
> # TABLE 삭제 생성  
> echo "delete hdfs path!!"  
> /data01/moneymall-shell/delete_hadoop_directory.sh /user/hive/warehouse/research.db/research_item;  
> echo "drop hive table"  
> hive -e "DROP TABLE IF EXISTS RESEARCH.ITEM";  
> echo "sqoop start!"  
> sqoop --options-file /data01/research-shell/sqoop/proc_input_clck.txt  
> echo "create RESEARCH.ITEM"  
> hive -e "CREATE EXTERNAL TABLE RESEARCH.ITEM(item_id STRING, std_ctg_id STRING, brand_id STRING  
> ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ','  
> LINES TERMINATED BY '\n'  
> STORED AS TEXTFILE LOCATION '/user/hive/warehouse/research.db/research_item'";  
> echo "hive start!"  
> /data01/moneymall-shell/delete_hadoop_directory.sh /user/hive/warehouse/research.db/temp_clck_item;  
> hive -f "/data01/research-shell/sql/proc_input_clck.sql";  
> 쿼리 파일.sql형식set hive.auto.convert.join=false;  
>   
> 쿼리  
> 예시set hive.auto.convert.join=false;  
>   
> DROP TABLE IF EXISTS RESEARCH.temp_clck_item;  
> 예시 쉘 호출 순서proc_clear.shproc_clear2.shproc_input_ord.shproc_input_clck.shproc_std_ctg_conf.shproc_shopp_std_ctg_conf.shproc_mbr_std_ctg_index_ord.shproc_mbr_std_ctg_index_clck.shproc_brand_conf.shproc_mbr_brand_index_ord.shproc_mbr_brand_index_clck.shproc_temp_table_drop.shproc_mbr_std_ctg_score.shproc_mbr_brand_score.shproc_temp_table_drop2.shproc_mbr_shopp_score.shproc_mbr_shopp_score_potential.shproc_temp_table_drop3.sh