---
Created: Invalid date
Updated: Invalid date
---
서버에 Hive 설치하고 metastore로 mariaDB 사용

Hive : [https://hive.apache.org/](https://hive.apache.org/)

1. **다운로드 :** cd /data01/hive wget [http://mirror.apache-kr.org/hive/hive-0.11.0/hive-0.11.0-bin.tar.gz](http://mirror.apache-kr.org/hive/hive-0.11.0/hive-0.11.0-bin.tar.gz)tar zxvf [hive-0.11.0-bin.tar.gz](http://mirror.apache-kr.org/hive/hive-0.11.0/hive-0.11.0-bin.tar.gz) /data01/hive/  
    # 다른 프로그램들은 해당 폴더 안에 압축파일 넣어 놓음  
    
2. **Hadoop 에 폴더 추가 및 권한변경**
    
    ```Plain
    $ hadoop fs -mkdir       /tmp
      $ hadoop fs -mkdir       /user/hive/warehouse
      $ hadoop fs -chmod g+w   /tmp
      $ hadoop fs -chmod g+w   /user/hive/warehouse
    ```
    
3. **설정파일 수정**cd hive-0.11.0-bin
    1. **hive-site.xml 수정**cp hive-default.xml.template hive-site.xmlvi hive-site.xml
        
        <configuration>
        
        <property>
        
        <name>javax.jdo.option.ConnectionURL</name>
        
        <value>jdbc:mysql://localhost/{MariaDB에서 사용할 DATABASE명}?createDatabaseIfNotExist=true</value> \#jdbc:mysql://localhost/HiveMetastoreDb?createDatabaseIfNotExist=true
        
        <description>JDBC connect string for a JDBC metastore</description>
        
        </property>
        
        <property>
        
        <name>javax.jdo.option.ConnectionDriverName</name>
        
        <value>com.mysql.jdbc.Driver</value>
        
        <description>Driver class name for a JDBC metastore</description>
        
        </property>
        
        <property>
        
        <name>javax.jdo.option.ConnectionUserName</name>
        
        <value>{mariaDB를 Hive Metastore로 사용할 때 사용하는 ID}</value> \#hive
        
        <description>username to use against metastore database</description>
        
        </property>
        
        <property>
        
        <name>javax.jdo.option.ConnectionPassword</name>
        
        <value>{위 ID에 해당하는 PASSWORD}</value> \#hive
        
        <description>password to use against metastore database</description>
        
        </property>
        
        </configuration>
        
    2. **hive-log4j.properties 수정**
        
        vi hive-log4j.properties
        
        hive.log.dir=/home/hive/{username}
        
    3. **.bashrc 수정**vi ~/.bashrc
        
        export HIVE_HOME=/bigdata/apps/hive
        
        PATH에 $HIVE_HOME/bin 추가
        
4. **Hive/lib 에 com.mysql.jdbc.Driver 넣어주기**
    
    mysql-connector-java-5.1.30-bin.jar
    
    wget [https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.30.tar.gz](https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.30.tar.gz)
    
5. **MariaDB에 Hive 에 metastore로 사용할 ID와 DATABASE 생성**
    1. 로그인 : mysql -u root -p
    2. 사용자 생성 : CREATE USER 'hive'@'%' IDENTIFIED BY 'hive';
    3. DataBase 생성 : CREATE DATABASE HiveMetastoreDb
    4. 권한부여 : grant all privileges on *.* to 'hive'@'localhost' with grant option;
    5. character set 수정 : alter database HiveMetastoreDb character set latin1
6. **Hive hwi 구성**
    1. conf/hive-site.xml 수정
        
        <property>
        
        <name>hive.hwi.listen.host</name>
        
        <value>0.0.0.0</value>
        
        <description>This is the host address the Hive Web Interface will listen on</description>
        
        </property>
        
        <property>
        
        <name>hive.hwi.listen.port</name>
        
        <value>9999</value>
        
        <description>This is the port the Hive Web Interface will listen on</description>
        
        </property>
        
        <property>
        
        <name>hive.hwi.war.file</name>
        
        <value>lib/hive-hwi.war</value> # 버전 맞게 수정
        
        <description>This sets the path to the HWI war file, relative to ${HIVE_HOME}.</description>
        
        </property>
        
    2. hwi 구동
        
        hive --service hwi
        
    3. localhost:9999/hwi 접속
7. **hive server로 구동하기**
    1. server에서 구동 : hive –service hiveserver
    2. client에서 server 접속 : hive -h {hive-serverIP} -p 10000
8. **TEST** 하둡 [start-all.sh](http://start-all.sh/) 되어 있어야 함
    1. TEST1hive; hive> show tables;마리아 DB의 metastore로 설정한 DATABASE에 안에 메타 관련 테이블들이 생성되었는지 확인
    2. TEST2 - hadoop 에서 hive로 데이터 이동할 경우 hadoop안의 대상 파일이 사라짐  
        $ hive;  
        hive> USE TESTHIVE;  
        1. **Hive안에 테이블 생성**  
            hive> CREATE EXTERNAL TABLE test2(  
            a STRING,b STRING,c STRING  
            ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ','LINES TERMINATED BY '\n';  
            
        2. **하둡 데이터를 Hive에 넣기**  
            hive> LOAD DATA INPATH '{HDFS안 폴더 경로}/testinfo.txt' INTO TABLE testinfo;  
            
        3. **로컬 데이터를 Hive에 넣기**hive> LOAD DATA LOCAL INPATH '/Users/zuhern/Downloads/testinfo2.txt' INTO TABLE testinfo;
        4. select * from test2;
        5. select count(*) from test2;
    3. TEST3 - hadoop 에서 hive로 데이터 이동할 경우 hadoop안의 대상 파일이 사라지지 않음
        1. CREATE EXTERNAL TABLE test3(id BIGINT, name STRING) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/{HDFS안 폴더 경로}/';
        2. select * from test3;
    4. TEST4 - Hive 안의 데이터를 로컬로 다운받기
        1. hive> insert overwrite local directory '다운받고 싶은 로컬 경로'  
            select * from testinfo;  
            
        2. 다운받은 파일 cat 으로 보거나 텍스트파일로 확인
    5. **테이블 삭제**
        1. DROP TABLE IF EXISTS test2;
9. **TEST 중 에러 발생 시**
    1. 에러 : FAILED: Error in metadata: java.lang.RuntimeException: Unable to instantiate org.apache.hadoop.hive.metastore.HiveMetaStoreClient FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask해결 : grant all privileges on *.* to 'hive'@'localhost' with grant option;
    2. 에러 : Specified key was too long; max key length is 767 bytes해결 : MariaDB [hiveuser]> alter database DATABASE명 character set latin1;