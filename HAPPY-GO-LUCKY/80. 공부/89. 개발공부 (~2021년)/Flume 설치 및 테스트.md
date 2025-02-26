---
Created: Invalid date
Updated: Invalid date
---
flume 문서[http://www.ashishpaliwal.com/blog/2013/12/flume-cookbook-quick-start/](http://www.ashishpaliwal.com/blog/2013/12/flume-cookbook-quick-start/)flume [http://flume.apache.org/](http://flume.apache.org/) - Compile the project

1. flume 다운로드
    1. flume을 소스로 받아서 사용하는 경우
        
        The Apache Flume build requires more memory than the default configuration. We recommend you set the following Maven options:
        
    2. bin.tart.gz을 다운받아서 사용하는 경우
2. flume_home 설정하기
3. flume의 config파일 수정하기
4. sink는 channel 이고  
    source는 channels 이다.  
    복사하거나 새파일을 만들기$ vi conf/test.properties $ cd /bigdata/apps/flume$ cp conf/flume-conf.properties.template conf/test.properties
5. test.properties 예제 내용\#source section
    
    producer.sources.s.type = netcat
    
    producer.sources.s.channels = c
    
    producer.sources.s.bind = localhost
    
    producer.sources.s.port = 44444
    
    \#source section
    
    producer.sources.s.type = seq
    
    producer.sources.s.channels = c
    
    \#source section
    
    producer.sources.s.type = exec
    
    producer.sources.s.command = tail -f /Users/zuhern/temp/test.txt
    
    producer.sources.s.channels = c
    
6. Test
    1. flume 실행
    2. 터미널 새 창 열어서
        
        아무 문자나 입력한 후 엔터 치고 flume 실행한 터미널 창으로 돌아오면 14/05/19 16:39:17 INFO sink.LoggerSink: Event: { headers:{} body: 68 65 6C 6C 6F hello }