---
Created: Invalid date
Updated: Invalid date
---
1. 하둡 다운로드

wget http://apache.mirror.cdnetworks.com/hadoop/common/stable1/hadoop-1.2.1-bin.tar.gz

2. 압축풀고 링크 걸기

tar zxvf hadoop-1.2.1-bin.tar.gz

ln -s hadoop-1.2.1 hadoop

3. HADOOP_HOME 등록하기

vi ~/.bash_profile

 export HADOOP_HOME=/home/bigdata/hadoop

PATH=$PATH:$HOME/bin:$HADOOP_HOME/bin

source .bash_profile

4. 하둡 설정 수정하기

cd ~/hadoop/conf

vi core-site.xml

<property>

<?xml version="1.0"?>

<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>

<!-- Put site-specific property overrides in this file. -->

<configuration>

<property>

<name>fs.default.name</name>

<value>hdfs://server01:9000</value>

</property>

<property>

<name>hadoop.tmp.dir</name>

<value>/home/bigdata/tmp</value>

</property>

</configuration>

vi hdfs-site.xml

<?xml version="1.0"?>

<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>

<!-- Put site-specific property overrides in this file. -->

<configuration>

<property>

<name>dfs.name.dir</name>

<value>/home/bigdata/filesystem</value>

</property>

<property>

<name>dfs.name.edits.dir</name>

<value>${dfs.name.dir}</value>

</property>

<property>

<name>dfs.http.address</name>

<value>server01:50070</value>

</property>

<property>

<name>dfs.secondary.http.address</name>

<value>server02:50090</value>

</property>

<property>

<name>dfs.data.dir</name>

<value>/home/bigdata/data/hdfs</value>

</property>

<property>

<name>dfs.replication</name>

<value>3</value>

</property>

</configuration>

 vi mapred-site.xml

<?xml version="1.0"?>

<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>

<!-- Put site-specific property overrides in this file. -->

<configuration>

<property>

<name>mapred.job.tracker</name>

<value>server01:9001</value>

</property>

<property>

<name>mapred.local.dir</name>

<value>${hadoop.tmp.dir}/mapred/local</value>

</property>

<property>

<name>mapred.system.dir</name>

<value>${hadoop.tmp.dir}/mapred/system</value>

</property>

</configuration>

vi hadoop-env.sh

export JAVA_HOME=/opt/jdk

export HADOOP_PID_DIR=/home/bigdata/pids

vi slaves

server02

server03

secondary namenode

vi masters

server02

5. 설정 끝낸 hadoop 폴더 압축해서 다른 서버에 보내고 링크걸어주기

6. 방화벽 모든서버에서

iptables -F

hadoop namenode -format

7. 확인

[zuhern@server01 ~]$ jps

1915 Jps

1119 NameNode

1296 JobTracker

[zuhern@server02 ~]$ jps

1942 SecondaryNameNode

2069 Jps

2020 TaskTracker

1858 DataNode

[zuhern@server03 ~]$ jps

1817 DataNode

1980 Jps

1911 TaskTracker