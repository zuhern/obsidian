---
Created: Invalid date
Updated: Invalid date
---
[http://zookeeper.apache.org/doc/r3.4.6/zookeeperStarted.html](http://zookeeper.apache.org/doc/r3.4.6/zookeeperStarted.html)

1. 설치
2. 설정파일 수정
3. conf폴더의 zoo_sample.cfg를 복사하여 zoo.cfg를 만든다cp conf/zoo_sample.cfg zoo.cfg vi zoo.cfg zoo.cfg 파일# The number of milliseconds of each ck tickTime=2000  
    # The number of ticks that the initial  
    # synchronization phase can takeinitLimit=10  
    # The number of ticks that can pass between  
    # sending a request and getting an acknowledgementsyncLimit=5  
    # the directory where the snapshot is stored.  
    # do not use /tmp for storage, /tmp here is just  
    # example sakes.dataDir=/tmp/zookeeper  
    # the port at which the clients will connectclientPort=2181  
    # the maximum number of client connections.  
    # increase this if you need to handle more clients  
    \#maxClientCnxns=60  
    #  
    # Be sure to read the maintenance section of the  
    # administrator guide before turning on autopurge.  
    #  
    \#   
    [http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance](http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance)  
    #  
    # The number of snapshots to retain in dataDir  
    \#autopurge.snapRetainCount=3  
    # Purge task interval in hours  
    # Set to "0" to disable auto purge feature  
    \#autopurge.purgeInterval=1server.1=127.0.0.1:2888:3888  
     dataDir=/tmp/zookeeper 위치에 myid파일을 생성한다.server.1=127.0.0.1:2888:3888 에서 server뒤에 1위치의 문자를 myid 파일에 적는다 
4. 시작[zkServer.sh](http://zkserver.sh/) start