---
Created: Invalid date
Updated: Invalid date
---
hadoop001

[moneymall@hadoop001 conf]$ vi zoo.cfg

# The number of milliseconds of each tick

tickTime=2000

# The number of ticks that the initial

# synchronization phase can take

initLimit=10

# The number of ticks that can pass between

# sending a request and getting an acknowledgement

syncLimit=5

server.1=zk001.prod.moneymall.ssgbi.com:2888:3888

server.2=zk002.prod.moneymall.ssgbi.com:2888:3888

server.3=zk003.prod.moneymall.ssgbi.com:2888:3888

# the directory where the snapshot is stored.

# do not use /tmp for storage, /tmp here is just

# example sakes.

dataDir=/data02/data/zookeeper

# the port at which the clients will connect

clientPort=2181

#

# Be sure to read the maintenance section of the

# administrator guide before turning on autopurge.

#

# [http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance](http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance)

#

# The number of snapshots to retain in dataDir

autopurge.snapRetainCount=3

# Purge task interval in hours

# Set to "0" to disable auto purge feature

autopurge.purgeInterval=1

[moneymall@storm001 conf]$ vi storm.yaml

transactional.zookeeper.root: "/transactional"

transactional.zookeeper.servers:

- "[storm001.prod.moneymall.ssgbi.com](http://storm001.prod.moneymall.ssgbi.com/)"

- "[storm002.prod.moneymall.ssgbi.com](http://storm002.prod.moneymall.ssgbi.com/)"

- "[storm003.prod.moneymall.ssgbi.com](http://storm003.prod.moneymall.ssgbi.com/)"