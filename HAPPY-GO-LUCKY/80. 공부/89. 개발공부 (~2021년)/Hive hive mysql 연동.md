---
Created: Invalid date
Updated: Invalid date
---
1. hive/conf/hive-site.xml 수정

4 <configuration> 5 6 <property> 7 <name>javax.jdo.option.ConnectionURL</name> 8 <value>jdbc:mysql://localhost/hive?createDatabaseIfNotExist=true</value> 9 <description>JDBC connect string for a JDBC metastore</description> 10 </property> 11 12 <property> 13 <name>javax.jdo.option.ConnectionDriverName</name> 14 <value>com.mysql.jdbc.Driver</value> 15 <description>Driver class name for a JDBC metastore</description> 16 </property> 17 18 <property> 19 <name>javax.jdo.option.ConnectionUserName</name> 20 <value>hive</value> 21 <description>username to use against metastore database</description> 22 </property> 23 24 <property> 25 <name>javax.jdo.option.ConnectionPassword</name> 26 <value>hive</value> 27 <description>password to use against metastore database</description> 28 </property> 29 </configuration>

2. mysql 에 해당 사용자 생성 한 후

3. 권한 부여

에러 :

FAILED: Error in metadata: java.lang.RuntimeException: Unable to instantiate org.apache.hadoop.hive.metastore.HiveMetaStoreClient  
FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask  

—— 해결

grant all privileges on *.* to 'hive'@'localhost' with grant option;

4. 테이블 수정

에러 :

Specified key was too long; max key length is 767 bytes

—— 해결

MariaDB [hiveuser]> alter database DATABASE명 character set latin1;

=========================================================================

참고 : [http://bigmark.tistory.com/35](http://bigmark.tistory.com/35)

리눅스 (우분투) 하둡 설치폴더로 이동 후 압축해제 한다.

압축 푼 것으로 설치는 완료되었으며,

설정을 해주어야 한다.

먼저 환경변수 등록을 해준다.

하둡 path 를 설정했던 .profile 로 이동

![[untitled 11.jpg|untitled 11.jpg]]

HIVE_HOME 경로 및 PATH 를 등록한다.

등록 저장 후 source .profile 로 적용

**Hive에서 사용할 HDFS 에 디렉토리 구성하기**

hive 실행하려면 하둡이 실행되어 있어야 한다.

hadoop 이 정상적으로 실행되면 다음 명령어로 hive를 실행한다.

hive가 정상 작동 하는지 확인

![[untitled 1 5.jpg|untitled 1 5.jpg]]

OK 가 떨어지면 제대로 설치 된것이다.

mysql 을 metastore 로 설정하려면 당연히 mysql 이 설치되어 있어야한다.

mysql 서비스를 시작한다.

루트 사용자의 암호를 설정한다.

위 명령어의 hiveid 는 사용자 아이디이며, hivepass 는 사용자 패스워드이다.

다음으로 metastore로 사용할 db를 생성한다.

기존 db를 사용하려면 안해도 무방하다.

HIVE_HOME/conf 에 hive-site.xml 을 생성 및 작성한다.

mysql connector 다운로드 [http://www.mysql.com/downloads/connector/j/](http://www.mysql.com/downloads/connector/j/)

다운로드한 mysql-connector-java-5.1.22.tar.gz 를 HIVE_HOME/lib/ 에 복사한다. (버전은 다를 수 있음)

mysql-connector-java-5.1.22.tar.gz 압축해제 하여 bin 폴더안에 있는 mysql-connector-java-5.1.22-bin.jar 파일만 넣으면 된다.

====================================================================================

# hive install and use mysql database metabase

**Tag**: the mysql, Hadoop, databases, path **Category**: [Database](http://www.databaseskill.com/345/1600346/) **Author**: zhyong880 **Date**: 2010-11-21

hive install and use mysql database metabase

Hive-0.8.0 Before installing the hive, pre-installed mysql for preservation metadata, install ant is used to enable HWI 1 namenode install the hive. Download and unzip the hive file into the hive / bin / under configuration [hive-config.sh](http://hive-config.sh/) file: export HADOOP_HOME = / home/hadoop/hadoop-0.20.203.0 export PATH =.: $ HADOOP_HOME / bin: $ PATH export HIVE_HOME = / home/hadoop/hive-0.8.0 export PATH = $ HIVE_HOME / bin: $ PATH export JAVA_HOME = / usr/java/jdk1.7.0_01 export JRE_HOME = / usr/java/jdk1.7.0_01/jre export CLASSPATH =.: $ JAVA_HOME / lib: $ JRE_HOME / lib: $ CLASSPATH export PATH =.: $ JAVA_HOME / bin: $ JRE_HOME / bin: $ PATH 2, added to the hive environment variable: export HIVE_HOME = / home/hadoop/hive-0.8.0 Created in mysql hadoop user password for hadoop, and create a metabase: mysql mysql> CREATE USER 'hadoop' @ 'master' IDENTIFIED BY 'hadoop'; mysql> GRANT ALL PRIVILEGES ON *. * TO 'hadoop' @ 'master' WITH GRANT OPTION; mysql> exit 4 file mysql-connector-java-5.1.15-bin.jar lib files directory. Otherwise an error: hive> show tables; FAILED: Error in metadata: javax.jdo.JDOFatalInternalException: Error creating transactional connection factory NestedThrowables: java.lang.reflect.InvocationTargetException FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask 5, in the hive / conf / folder, the new hive-site.xml file, and copy the entire contents into the the hive-default.xml.template the following modifications: (Using mysql as a meta-database) <property> <name> [hive.metastore.local](http://hive.metastore.local/) </ name> <value> true </ value> </ Property> <property> <name> javax.jdo.option.ConnectionURL </ name> <! - <value> Jdbc: derby:; databaseName = metastore_db; create = true </ value> -> <value> jdbc: mysql :/ / master: 3306/metastore </ value> <description> JDBC connect string for a JDBC metastore </ description> </ Property> <property> <name> javax.jdo.option.ConnectionDriverName </ name> <value> com.mysql.jdbc.Driver </ value> <description> Driver class name for a JDBC metastore </ description> </ Property> <property> <name> javax.jdo.option.ConnectionUserName </ name> <value> hadoop </ value> <description> username to use against metastore database </ description> </ Property> <property> <name> javax.jdo.option.ConnectionPassword </ name> <value> hadoop </ value> <description> password to use against metastore database </ description> </ Property> Create several directories in HDFS $ HADOOP_HOME / bin / hadoop fs-mkdir / tmp $ HADOOP_HOME / bin / hadoop fs-mkdir / user / hive / warehouse $ HADOOP_HOME / bin / hadoop fs-chmod g+ w / tmp $ HADOOP_HOME / bin / hadoop fs-chmod g+ w / user / hive / warehouse 7, the start hive Start hive: $ HIVE_HOME / bin / hive 8 start hwi interface: export ANT_LIB = / opt / ant / lib bin / hive - service hwi bin / hive - service hwi - help 9, in the hive command-line mode, use the show TABLES; test mysql connection is correct. Mysql metadata alter database hive character set latin1 So as not at **max key length is 767 bytes** com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: Specified **key** was too long; **max key length is767 bytes** 

**[출처]** [hive & mysql 연동](http://blog.naver.com/khh141/60199484423)|**작성자** [콩이](http://blog.naver.com/khh141)