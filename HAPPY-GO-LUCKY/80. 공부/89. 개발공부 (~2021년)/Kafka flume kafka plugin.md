---
Created: Invalid date
Updated: Invalid date
---
[http://beyondj2ee.wordpress.com/2013/09/15/flumeng-kafka-plugin-%ED%94%8C%EB%9F%BC%EC%B9%B4%ED%94%84%EC%B9%B4-%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8/](http://beyondj2ee.wordpress.com/2013/09/15/flumeng-kafka-plugin-%ED%94%8C%EB%9F%BC%EC%B9%B4%ED%94%84%EC%B9%B4-%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8/)

Flume의 Sink와 Kafka의 Producer를 합친 클래스Flume Source -> Flume Channel -> Flume Sink + Kafka Producer -> Kafka broker -> Kafka ConsumerFlume Start : flume-ng agent --conf-file 파일경로 --name 에이젼트명  
  
ex) flume-ng agent --conf-file /bigdata/apps/flume/conf/irtms.properties --name producername : irtms.properties안에 선언된 agent명Flume Sink + Kafka Producer Class  
  
configure() : 프로퍼티 파일에서 프로퍼티 읽어오기 (kafka에 필요한 프로퍼티)  
  
metadata.broker.list : brokerIP:port (ex) broker1:9092, broker2:9092serializer.class : (ex) kafka.serializer.DefaultEncodepartitioner.class : (ex) kafka.producer.DefaultPartitionerrequest.required.acks : 1  
  
0 : broker로 부터 받았다는 통지를 받음의 여부를 신경쓰지 않음 (default)1 : leader 복제본이 데이터를 받았다는 통지를 받아야 함-1 : 모든 동기 복제본들도 데이터를 받았다는 통지를 받음start() : ProducerConfig 객체 생성하기 (프로퍼티 정보 담아서)  
  
Producer 객체 생성하기 (ProducerConfig 담아서)process() : Status : 상태 정보  
  
Channel 객체 생성후 해당 객체로 트랜잭션 객체 뽑아내어 트랜잭션 관리confiugure() 에서 받은 프로퍼티 정보 읽기 (producer 정보)partitionKey : 정보를 보낼 파티션 키encoding : 인코딩 정보topic : 토픽 name  
  
Channel 에서 받은 이벤트를 프로퍼티의 인코딩 정보로 이벤트를 인코딩 한다.KeyedMessage<String, String> 객체 생성 (topic, partitionKey, message);producer.send(keyedMessage); 로 이벤트를 보내고트랜잭션 Commit (에러시 rollBack)status = ready (에러시 backOff)mvn -e -DskipTests clean install assembly:single -nsutarget의 assy.jar를 flume의 plugins.d/agent/lib에 옮김  
  
ex) /bigdata/apps/flume/plugins.d/agent/libflume구동시 사용할 .propertiesproducer propertyproducer.sources.s.channels = c  
producer.sinks.r.channel = c  
\#source section  
\#producer.sources.s.type = seq  
\#producer.sources.s.type=netcat  
\#producer.sources.s.bind=localhost  
\#producer.sources.s.port=51000  
producer.sources.s.type=exec  
producer.sources.s.command=tail -F /Users/zuhern/temp/test.txt  
producer.sources.s.restart=true  
producer.sources.s.restartThrottle=10000  
# Each sink's type must be definedproducer.sinks.r.type = com.willbe.flume.sink.KafkaSinkproducer.sinks.r.metadata.broker.list=127.0.0.1:9092producer.sinks.r.partition.key=0producer.sinks.r.partitioner.class=com.willbe.kafka.partitioner.SinglePartitionerproducer.sinks.r.serializer.class=kafka.serializer.StringEncoderproducer.sinks.r.request.required.acks=0producer.sinks.r.max.message.size=1000000producer.sinks.r.producer.type=syncproducer.sinks.r.custom.encoding=UTF-8[producer.sinks.r.custom.topic.name](http://producer.sinks.r.custom.topic.name/)=kafkaTest  
# Each channel's type is defined.  
producer.channels.c.type = memory  
producer.channels.c.capacity = 1000  
\#producer.channels.c.transactionCapacity = 1000  
\#producer.channels.c.byteCapacityBufferPercentage = 20  
\#producer.channels.c.byteCapacity = 80000  

`1. 주키퍼 서버 스타트`

`zkServer.sh start`

`2. 카프카 서버 스타트`

`kafka-server-start.sh /bigdata/apps/kafka/config/server.properties`

`3. 프로젝트 빌드 및 라이브러리 이동`

`cd study-flumeng-kafka-plugin/`

`mvn package`

`cp flumeng-kafka-plugin/libs/*.jar /bigdata/apps/flume/plugins.d/agent/libext`

`cp flumeng-kafka-plugin/package/flumeng-kafka-plugin.jar /bigdata/apps/flume/plugins.d/agent/lib`

`- conf 파일을 프로젝트에서 관리할 때`

`cp flumeng-kafka-plugin/conf/flume-conf.properties /bigdata/apps/flume/conf/`

`4. 플럼 실행`

`flume-ng agent --conf-file /bigdata/apps/flume/conf/flume-conf.properties --name producer`

`5. 토픽 보기`

`kafka-list-topic.sh --zookeeper localhost:2181`

`6. 카프카 컨슈머에 데이터 오나 확인`

`kafka-console-consumer.sh --zookeeper localhost:2181 --topic kafkaTopic --from-beginning`

`카프카 config`

`/bigdata/apps/kafka/config/server.properties 의 주키퍼 포트 localhost:2181`

`/bigdata/apps/kafka/config/server.properties 의 카프카 포트 9092`

`플럼 conf 파일`

`kafka포트`

`kafka Topic`

`7. config`

`1)`

`producer.sinks.r.serializer.class=kafka.serializer.StringEncoder`

`를 빼면 아래 에러난다.`

`Caused by: org.apache.flume.ChannelException: Space for commit to queue couldn't be acquired Sinks are likely not keeping up with sources, or the buffer size is too tight`

`INFO ({SinkRunner-PollingRunner-DefaultSinkProcessor} KafkaSink.java[process]:114) [2014-05-23 10:29:15,511] - Send Message to Kafka : [3454] -- [{ headers:{} body: 33 34 35 34 3454 }]`

`INFO ({SinkRunner-PollingRunner-DefaultSinkProcessor} KafkaSink.java[process]:114) [2014-05-23 10:29:56,268] - Send Message to Kafka : [943] -- [{ headers:{} body: 39 34 33 943 }]`

`INFO ({SinkRunner-PollingRunner-DefaultSinkProcessor} KafkaSink.java[process]:114) [2014-05-23 10:31:52,958] - Send Message to Kafka : [0] -- [{ headers:{} body: 30 0 }]`

`2)`

`producer.sinks.r.partitioner.class=org.apache.flume.plugins.SinglePartition`

`가 있으면 flume으로 들어오는 데이터가 바로바로 kafka consumer에 들어오는데`

`이걸 빼면 한참 뒤에 들어오거나 다시 consumer를 다시 올려야지 데이터가 들어온다???`

`또 아닌 것 같기도 하고,.. 초반에 만 그런듯..?`