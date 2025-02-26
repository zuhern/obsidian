---
Created: Invalid date
Updated: Invalid date
---
/////// jobtracker 등록 ////////

SET mapred.job.tracker=local;

SET mapred.job.tracker=10.203.5.21:9001; //hdfs-site.xml

/////// hadoop 에서 hive table로 데이터 넣기 ////////

zuhernui-MacBook-Pro:~ zuhern$ hive  
Logging initialized using configuration in jar:file:/bigdata/apps/hadoop-1.2.1/lib/hive-common-0.11.0.jar!/hive-log4j.properties  
Hive history file=/tmp/zuhern/hive_job_log_zuhern_2586@zuhernui-MacBook-Pro.local_201404030033_944610403.txt  
2014-04-03 00:33:32.223 java[2586:1903] Unable to load realm info from SCDynamicStore  

hive> CREATE DATABASE TESTHIVE;  
OK  
Time taken: 2.332 seconds  

hive> show databases;  
OK  
default  
testhive  
Time taken: 0.136 seconds, Fetched: 2 row(s)  

hive> USE TESTHIVE;  
OK  
Time taken: 0.014 seconds  

hive> CREATE EXTERNAL TABLE testinfo(a STRING,b STRING,c STRING)ROW FORMAT DELIMITED FIELDS TERMINATED BY ','LINES TERMINATED BY '\n’;

OK  
Time taken: 0.313 seconds  

// core-site.xml  
hive> LOAD LOCAL DATA INPATH '/user/zuhern/test/testinfo.txt' INTO TABLE testinfo;  

Loading data to table testhive.testinfo  
Table testhive.testinfo stats: [num_partitions: 0, num_files: 1, num_rows: 0, total_size: 36, raw_data_size: 0]  
OK  
Time taken: 0.299 seconds  

hive> select * from testinfo;

OK  
aaabbbccc  
dddeef  
ghi  
jjkklll  
Time taken: 0.198 seconds, Fetched: 4 row(s)  
hive>  

///////// hive 에서 데이터 파일로 만들기 //////////

//--- Hive 테이블의 데이터를 외부 파일로 저장  
insert overwrite [local] directory '~' //--- overwrite 대신 into 사용 가능 select ~;  

hive> insert overwrite local directory '/Users/zuhern/Downloads/testout'

select * from testinfo;

INSERT OVERWRITE LOCAL DIRECTORY '/Users/zuhern/Downloads/testout’

SELECT COUNT(*) AS cnt from test info

;

cat 으로 보기

**[출처]** [[hive] 중복을 제외한( group by ) 집계함수( count )와 이를 이용한 정렬 ( order by ) 를 파일로 빼내기](http://blog.naver.com/01191449527/205790647) |**작성자** [01191449527](http://blog.naver.com/01191449527)

///////// hive server 에 접속하기 /////////

hive -h 10.149.188.160 -p 10000

[http://www.bicdata.com/bbs/board.php?bo_table=develop_groupstudy&wr_id=405](http://www.bicdata.com/bbs/board.php?bo_table=develop_groupstudy&wr_id=405)

LOAD DATA LOCAL INPATH '/user/moneymall/temp/testdata.txt' INTO TABLE test;