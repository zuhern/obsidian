---
Created: Invalid date
Updated: Invalid date
---
1. kafka 다운로드
2. 실행 및 테스트
    1. kafka 실행하기 (kafka 경로 안에서)
    2. topic 생성하기
    3. list 보기
    4. producer test 하기
    5. 이때 에러가 날경우 kafka 0.8.0 버전에서 lib/slf4j* 를 현재 카프카 libs에 복사하니까 해결됨..
    6. consumer test 하기
3. 실행 및 테스트 (broker 여러개)
    1. 서버 2개 올리기  
        config/server.properties 복사해서 server-1 server-2 만들고  
        broker.id  
        
        port  
        log.dir  
        다른 서버 정보와 겹치지 않게 수정  
        
    2. The JMX ports are used for optional monitoring and troubleshooting with tools such as JConsole.
    3. topic 생성하기
    4. list 보기
    5. producer test 하기
    6. consumer test 하기
    7. topic 추가 수정 삭제
    8. To add configs: > bin/kafka-topics.sh --zookeeper zk_host:port/chroot --alter --topic my_topic_name --config x=y remove a config: > bin/kafka-topics.sh --zookeeper zk_host:port/chroot --alter --topic my_topic_name --deleteConfig xdeleting a topic: > bin/kafka-topics.sh --zookeeper zk_host:port/chroot --delete --topic my_topic_name