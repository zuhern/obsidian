---
Created: Invalid date
Updated: Invalid date
---
```Plain
hive 에러
```

```Plain
show tables;
```

```Plain
notfoundclasses 뜨면 hadoop conf 안에 hdfs-site.xml, mapred-site.xml, core-site.xml
```

```Plain
안에 필요하지 않은 것들 지우기
```

```Plain
- 나는 lzo 안 깔려있는데 lzo 관련 프로퍼티가 있어서..
```

```Plain
hdfs랑 mapred 맨 밑 두개 프로퍼티 삭제
```

```Plain
================================================================================
```

```Plain
http://mimul.com/pebble/default/2011/12/21/1324466112240.html
```

HiveQL로 정의한 쿼리문을 통해 Hive가 맵리듀스잡으로 변환한 뒤 실행하여 처리하게 됩니다. 즉, SQL과 유사한 언어로 MapReduce잡을 실행하는 툴이죠.  
그래서 Hive는 SQL의 지식을 알고 있는 사람이라면 친숙하게 받아들일 수 있는 장점이 있다고 말할 수 있습니다.   
$ $HADOOP_HOME/bin/hadoop fs -mkdir /tmp $ $HADOOP_HOME/bin/hadoop fs -mkdir /user/hive/warehouse $ $HADOOP_HOME/bin/hadoop fs -chmod g+w /tmp $ $HADOOP_HOME/bin/hadoop fs -chmod g+w /user/hive/warehouse  
**1. Mysql이 설치되어 있어야 함** 

```Plain
- create database hive;
 - grant all on hive.* to 'hiveuser'@'localhost' identified by 'hivepw';
 - flush privileges;
```

**2. Hive 설치**

> [http://mirror.khlug.org/apache//hive/hive-0.8.0/hive-0.8.0.tar.gz](http://mirror.khlug.org/apache//hive/hive-0.8.0/hive-0.8.0.tar.gz)  
> tar xvfz hive-0.8.0.tar.gz  
> ln -s hive-0.8.0 hive  
> cd hive/lib/  
> wget  
[http://www.mimul.com/hadoop/mysql-connector-java-5.1.11.jar](http://www.mimul.com/hadoop/mysql-connector-java-5.1.11.jar)  
> cd ../conf  
> cp hive-default.xml.template hive-default.xml  
> cp hive-log4j.properties.template hive-log4j.properties  
> cp hive-exec-log4j.properties.template hive-exec-log4j.properties  
> vi hive-default.xml 설정 변경 javax.jdo.option.ConnectionURL jdbc:mysql://localhost:3306/hive?createDatabaseIfNotExist=true javax.jdo.option.ConnectionDriverName com.mysql.jdbc.Driver javax.jdo.option.ConnectionUserName hiveuser javax.jdo.option.ConnectionPassword hivepw  
> vi ~/.bash_profile  
HIVE_HOME=/database/server/hive;export HIVE_HOME  
HIVE_CONF_DIR=/database/server/hive/conf;export HIVE_CONF_DIR  
PATH에 $HIVE_HOME/bin 추가  

**3. 데이터 다운로드**

> cd movielens  
> wget  
[http://www.grouplens.org/system/files/hetrec2011-movielens-2k.zip](http://www.grouplens.org/system/files/hetrec2011-movielens-2k.zip)  
> cat user_ratedmovies-timestamps.dat | sed'/^I/,/g' > user_ratedmovies-timestamps1.dat  
> mv user_ratedmovies1-timestamps.dat user_ratedmovies-timestamps.dat  
> hadoop fs -put user_ratedmovies-timestamps.dat /data  

**4. Hive 사용기**

> hive  
hive> show tables;  
OK  
Time taken: 2.753 seconds  
hive> create table rating (userid INT, movieid INT, rating FLOAT, ds STRING) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' STORED AS TEXTFILE;  
OK  
Time taken: 0.424 seconds  
hive> show TABLES;  
OK  
rating  
Time taken: 0.093 seconds  
hive> describe rating;  
OK  
userid int  
movieid int  
rating float  
ds string  
Time taken: 2.258 seconds  
hive> LOAD DATA INPATH '/data/user_ratedmovies-timestamps.dat' OVERWRITE INTO TABLE rating;  
Loading data to table default.rating  
Deleted hdfs://mimul:9000/user/hive/warehouse/rating  
OK  
Time taken: 0.369 seconds  
hive> select count(*) from rating r;  
Total MapReduce jobs = 1  
Launching Job 1 out of 1  
Number of reduce tasks determined at compile time: 1  
In order to change the average load for a reducer (in bytes): set hive.exec.reducers.bytes.per.reducer=<number>  
In order to limit the maximum number of reducers: set hive.exec.reducers.max=<number>  
In order to set a constant number of reducers: set mapred.reduce.tasks=<number>  
Starting Job = job_201112192049_0028, Tracking URL =  
[http://mimul:50030/jobdetails.jsp?jobid=job_201112192049_0028](http://mimul:50030/jobdetails.jsp?jobid=job_201112192049_0028)  
Kill Command = /database/server/hadoop-0.20.205.0/bin/../bin/hadoop job -Dmapred.job.tracker=mimul:9001 -kill job_201112192049_0028  
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1  
2011-12-21 17:59:25,177 Stage-1 map = 0%, reduce = 0%  
2011-12-21 17:59:31,258 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:32,273 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:33,283 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:34,293 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:35,303 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:36,313 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:37,323 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:38,332 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:39,343 Stage-1 map = 100%, reduce = 0%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:40,353 Stage-1 map = 100%, reduce = 33%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:41,362 Stage-1 map = 100%, reduce = 33%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:42,372 Stage-1 map = 100%, reduce = 33%, Cumulative CPU 2.28 sec  
2011-12-21 17:59:43,386 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 4.93 sec  
2011-12-21 17:59:44,392 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 4.93 sec  
2011-12-21 17:59:45,402 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 4.93 sec  
2011-12-21 17:59:46,412 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 4.93 sec  
2011-12-21 17:59:47,422 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 4.93 sec  
2011-12-21 17:59:48,540 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 4.93 sec  
2011-12-21 17:59:49,553 Stage-1 map = 100%, reduce = 100%, Cumulative CPU 4.93 sec  
MapReduce Total cumulative CPU time: 4 seconds 930 msec  
Ended Job = job_201112192049_0028  
MapReduce Jobs Launched:  
Job 0: Map: 1 Reduce: 1 Accumulative CPU: 4.93 sec HDFS Read: 24386850 HDFS Write: 7 SUCESS  
Total MapReduce CPU Time Spent: 4 seconds 930 msec  
OK  
855598  
Time taken: 34.157 seconds  
hive> quit;  
[mimul]/database/samples/hive> cat user_ratedmovies-timestamps.dat | wc -l 855598</number></number></number>  
  
-------------------------------------------------------------------------------------------  
  
위와 같이 설치 후 hive 실행시 아래와 같은 에러가 발생하면  
  
Exception in thread "main" java.lang.NoClassDefFoundError: org/apache/hadoop/hive/conf/HiveConfat java.lang.Class.forName0(Native Method)at java.lang.Class.forName(Class.java:247)at org.apache.hadoop.util.RunJar.main(RunJar.java:149)Caused by: java.lang.ClassNotFoundException: org.apache.hadoop.hive.conf.HiveConfat java.net.URLClassLoader$1.run(URLClassLoader.java:200)at java.security.AccessController.doPrivileged(Native Method)at java.net.URLClassLoader.findClass(URLClassLoader.java:188)at java.lang.ClassLoader.loadClass(ClassLoader.java:307)at java.lang.ClassLoader.loadClass(ClassLoader.java:252)at java.lang.ClassLoader.loadClassInternal(ClassLoader.java:320)... 3 morehadoop-env.sh에 HADOOP_CLASSPATH를 아래와 같이 수정해 준후 실행하면 된다.  
  
export HADOOP_CLASSPATH=${HADOOP_CLASSPATH}:${HBASE_HOME}:${HBASE_HOME}/hbase-0.92.0.jar:${HBASE_HOME}/conf

**[출처]** [Apache Hive 맛보기](http://blog.naver.com/ggaibi1004/10133063844)|**작성자** [깨비ya](http://blog.naver.com/ggaibi1004)

**[출처]** [Apache Hive 맛보기](http://blog.naver.com/ggaibi1004/10133063844)|**작성자** [깨비ya](http://blog.naver.com/ggaibi1004)