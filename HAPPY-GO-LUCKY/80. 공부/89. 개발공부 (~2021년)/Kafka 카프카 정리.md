---
Created: Invalid date
Updated: Invalid date
---
1. Kafka
    1. 분산
    2. 분할
    3. 복제
    4. 설정된 기간 내에는 소비여부와 관계없이 메세지를 저장하고, 그 후 삭제된다.
    5. 키를 사용하여 데이터를 분할
2. producer
    1. producer를 통해 메세지를 publish한다.
    2. producer가 topic의 어느 partition에 할당할 것인지 정한다
        1. 라운드 로빈으로 균형있게 분배할 수 있다.
        2. partition function으로 Key를 이용해서 분배할 수 있다. 이 방식을 더 많이 쓴다.
3. consumer
    1. topic에 맞는 데이터를 읽어온다.
    2. 각 consumer는 자신이 소비한 log의 offset정보를 가지고 있는다. 어디까지 받았는지.
    3. consumer가 offset정보를 제어한다. 예로 reprocess 시에는 offset정보를 reset 할 수 있다.
    4. 다른 consumer에 영향을 끼치지 않는다.
4. consumer group
    1. 메세징의 기존 모델은 [queuing](http://en.wikipedia.org/wiki/Message_queue) and [publish-subscribe](http://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern).  
        queuing : 메세지를 보낸 곳이 어딘지를 consumer가 알고 전달되는듯. publish-subscribe는 모든 consumer에 메세지를 전달하고 그 메세지를 받을지는 consumer가 선택  
        consumer group은 이 둘을 종합함  
        consumer는 consumer group name을 가지고 있고, topic을 통해 오는 메세지들은 각각 consumer group의 하나의 consumer에 전달된다.  
        
    2. consumer는 분리된 프로세스나 분리된 서버에 있어도 된다.
    3. 하나의 partition안에서는 메세지 순서를 유지하나, 둘 이상의 파티션일 경우 전체의 순서는 섞인다.토픽의 전체의 데이터의 순서가 유지되길 바란다면 파티션을 하나만 두어야 한다. consumer가 하나 이더라도.
5. broker
    1. broker라 불리는 하나이상의 서버로 구성되어 있다.
6. topic
    1. 카프카는 topic으로 메세지의 범주를 나눈다.
7. offset
    1. 각 파티션 안의 메세지는 순차적이고 유니크한 id가 부여되며 이를 offset이라고 한다.
8. partition
    1. The partitions in the log serve several purposes.
    2. 싱글서버에 맞는 사이즈보다 큰 로그를 사용하기 위해서, topic이 많은 partition을 가지면 많은 양의 데이터를 처리할 수 있다.
    3. 병렬처리를 하기 위해서 Second they act as the unit of parallelism—more on that in a bit.

- Partitions are now replicated. Previously the topic would remain available in the case of server failure, but individual partitions within that topic could disappear when the server hosting them stopped. If a broker failed permanently any unconsumed data it hosted would be lost. Starting with 0.8 all partitions have a replication factor and we get the prior behavior as the special case where replication factor = 1. Replicas have a notion of committed messages and guarantee that committed messages won't be lost as long as at least one replica survives. Replica logs are byte-for-byte identical across replicas.
- Producer and consumer are replication aware. When running in sync mode, by default, the producer send() request blocks until the messages sent is committed to the active replicas. As a result the sender can depend on the guarantee that a message sent will not be lost. Latency sensitive producers have the option to tune this to block only on the write to the leader broker or to run completely async if they are willing to forsake this guarantee. The consumer will only see messages that have been committed.
- The consumer has been moved to a "long poll" model where fetch requests block until there is data available. This enables low latency without frequent polling. In general end-to-end message latency from producer to broker to consumer of only a few milliseconds is now possible.
- We now retain the key used in the producer for partitioning with each message, so the consumer knows the partitioning key.
- We have moved from directly addressing messages with a byte offset to using a logical offset (i.e. 0, 1, 2, 3...). The offset still works exactly the same - it is a monotonically increasing number that represents a point-in-time in the log - but now it is no longer tied to byte layout. This has several advantages: (1) it is asthetically nice, (2) it makes it trivial to calculate the next offset or to traverse messages in reverse order, (3) it fixes a corner case interaction between consumer commit() and compressed message batches. Data is still transferred using the same efficient zero-copy mechanism as before.
- We have removed the zookeeper dependency from the producer and replaced it with a simple cluster metadata api.
- We now support multiple data directories (i.e. a JBOD setup).
- We now expose both the partition and the offset for each message in the high-level consumer.
- We have substantially improved our integration testing, adding a new integration test framework and over 100 distributed regression and performance test scenarios that we run on every checkin.