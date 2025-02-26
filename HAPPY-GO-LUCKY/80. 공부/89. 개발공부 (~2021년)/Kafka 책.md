---
Created: Invalid date
Updated: Invalid date
---
빅데이터의 과제는 1. 대용량의 데이터를 모으고 2. 이를 분석하는 것이다.

카프카는 정보와의 원활한 통합을 제공 정보의 생산을 차단하지 않고 생산자와 소비자의, 생산자는 최종 소비자가 누구인지 알리지 않고.

지속적인 메세징,

높은 처리량,

분산

다양한클라이언트지원

실시간

**Persistent messaging**: To derive the real value from big data, any kind  
of information loss cannot be afforded. Apache Kafka is designed with **O(1)** disk structures that provide constant-time performance even with very large volumes of stored messages, which is in order of TB.**High throughput**: Keeping big data in mind, Kafka is designed to work on commodity hardware and to support millions of messages per second.**Distributed**: Apache Kafka explicitly supports messages partitioning over Kafka servers and distributing consumption over a cluster of consumer machines while maintaining per-partition ordering semantics.**Multiple client support**: Apache Kafka system supports easy integration of clients from different platforms such as Java, .NET, PHP, Ruby, and Python.

**Real time**: Messages produced by the producer threads should be immediately visible to consumer threads; this feature is critical to event-based systems such as **Complex Event Processing** (**CEP**) systems.

- [x] 밑에 꺼 없음… -> 0.7.*에는 있음

The following command downloads all the dependencies such as Scala compiler, Scala libraries, Zookeeper, Core-Kafka update, and Hadoop consumer/producer update, for building Kafka: [root@localhost opt]#./sbt update

- [x] 책에선 console-producer, consumer.. kafka 로그 찍히던데.. 내껀 안찍힘
- [x] env JMX_PORT=10000 bin/kafka-server-start.sh config/server-2.properties <=== JMX??????

The JMX ports are used for optional monitoring and troubleshooting with tools such as JConsole.

**bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication 2 --partition 2 --topic other topic**

**broker를 3개 띄운상태에서 2개를 쓴다고 하면 랜덤으로 배정되는 건가???**

**——>>>>> bin/kafka-console-producer.sh --broker-list localhost:9092,localhost:9093 --topic other topic 로 broker를 지정하는 것인 듯**

If we have a requirement to run multiple producers connecting to different combinations of brokers, we need to specify the broker list for each producer like we did in the case of multiple brokers.

- [x] multiple node…. 노드가 뭔지 잘 안 와닿음. single node에 multiple broker는 서버 한대에 여러개의 broker를 띄우는 것이니까…. kafka-server-start 하고 설정 다른 properties로 ..
- [x] server.properties 에 적는 zookeeper.connect에 관한 설명임

This specifies the ZooKeeper's connection localhost:2181 string in the form hostname:port/

chroot. Here, chroot is a base directory  
that is prepended to all path operations  

(this effectively namespaces all Kafka znodes to allow sharing with other applications on the same ZooKeeper cluster).

Chapter 4

- Kafka design fundamentals 카프카 디자인 기초
- Message compression in Kafka 카프카에서 메세지 압축
- Cluster mirroring in Kafka 카프카에서 클러스터 미러링
- Replication in Kafka 카프카에서의 복제

- [x] By Kafka design, the message state of any consumed message is maintained within the message consumer, and the Kafka broker does not maintain a record of what is consumed by whom, which also means that poor designing of a custom consumer ends up in reading the same message multiple times.

카프카는 마스터 개념이 없다. 주키퍼가 관리한다.

동기 복제 : 리더와 팔로워들이 데이터를 받고 팔로워들이 리더에게 승인(?)을 보내고 리더가 프로듀서에게 승인을 보낸다.

비동기 복제 : 팔로워들이 리더에게 승인을 보내던 말던 리더가 메세지를 다 받으면 프로듀서에게 승인을 보낸다.

- [x] java SimpleProducer kafkatopic Hello_There 37페이지 ) 이거 무슨 컴파일하고 돌리는거 어찌하는지 모르겠다..ㅡㅡ;;
- [x] HighLevel, Simple Consumer 차이 잘 모르겠ㄷ…ㅠㅠㅠ
- [x] offset이 뭔지도 잘 모르겠다

Each partition is an ordered, immutable sequence of messages that is continually appended to—a commit log. The messages in the partitions are each assigned a sequential id number called the offset that uniquely identifies each message within the partition.

- [x] **Multithreaded consumer for multipartition topics**

The previous example is a very basic example of a consumer who consumes messages from a single broker with no explicit partitioning of messages within  
the topic. Let's jump to the next level and write another program, which consumes messages from multiple partitions connecting to single/multiple topics.  

A multithreaded high-level consumer-API-based design is usually based on the number of partitions in the topic and follows a one-to-one mapping approach between the thread and the partitions within the topic. For example, if four partitions are defined for any topic, as a best practice, only four threads should be initiated with the consumer application to read the data; otherwise some conflicting behavior, such as threads never receiving a message or thread receiving messages from multiple partitions, may occur. Also, receiving multiple messages will not guarantee that the messages will be placed in order. For example, a thread may receive two messages from the first partition and three from the second partition, then three more from the first partition, followed by some more from the first partition, even

if the second partition has data available.

- [x] 위에 꺼 예제에 executor?왜있는건지..역할이 뭔지 모르겠음

ㅇㅇ

ㅇㄹ