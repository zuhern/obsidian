---
Created: Invalid date
Updated: Invalid date
---
# 1. 소개

Flume은 클라우데라에서 개발된 오픈소스 로그 수집 소프트웨어로 아파치 인큐베이터를 통하여 안정화를 거치며 Flume-NG로 명명되었으며 데이터 수집을 위한 프레임워크로 다양한 로그 데이터 수집 및 모니터링이 가능하고 실시간 전송을 지원한다. 자바로 구현되어 있기 때문에 다양한 운영체제에 설치가 가능하다. 노드의 추가 및 관리가 손쉽고 분산처리 시스템의 로그수집에 적합하여 Hadoop과 잘 어울린다. 최신버전은 Flume-NG 1.4.0(2013.12월) 이다.

![[untitled 9.jpg|untitled 9.jpg]]

[그림 flume-ng 구조]

### Flume-NG 구성

- Event
    
    Flume에서 전달되는 데이터의 단일단위
    
- Source
    
    이벤트를 발생시키는 대상을 정의
    
- Channel
    
    최종 목적지인 sink로 전달하기 위한 임시 저장소
    
- Sink
    
    Sink는 Channel에서 이벤트를 하나씩 꺼내어 저장소에 저장하는 역할
    

# 2. 설치

### 1. 다운로드

```Plain
http://ftp.daum.net/apache/flume/1.4.0/apache-flume-1.4.0-bin.tar.gz
```

### 2. 환경변수 설정

```Plain
$ vi ~/.bash_profile
# Flume
export FLUME_HOME=/home/hadoop/apache-flume-1.4.0-bin
export PATH=$PATH:$FLUME_HOME/bin
$ source ~/.bash_profile
```

### 3. Flume Configuration

```Plain
http://www.apache.org/licenses/LICENSE-2.0
```

### 4. Help

```Plain
$ flume-ng help
Usage: /home/hadoop/apache-flume-1.4.0-bin/bin/flume-ng <command> [options]...

commands:
  help                  display this help text
  agent                 run a Flume agent
  avro-client           run an avro Flume client
  version               show Flume version info

global options:
  --conf,-c <conf>      use configs in <conf> directory
  --classpath,-C <cp>   append to the classpath
  --dryrun,-d           do not actually start Flume, just print the command
  --plugins-path <dirs> colon-separated list of plugins.d directories. See the
                        plugins.d section in the user guide for more details.
                        Default: $FLUME_HOME/plugins.d
  -Dproperty=value      sets a Java system property value
  -Xproperty=value      sets a Java -X option

agent options:
  --conf-file,-f <file> specify a config file (required)
  --name,-n <name>      the name of this agent (required)
  --help,-h             display help text

avro-client options:
  --rpcProps,-P <file>   RPC client properties file with server connection params
  --host,-H <host>       hostname to which events will be sent
  --port,-p <port>       port of the avro source
  --dirname <dir>        directory to stream to avro source
  --filename,-F <file>   text file to stream to avro source (default: std input)
  --headerFile,-R <file> File containing event headers as key/value pairs on each new line
  --help,-h              display help text

  Either --rpcProps or both --host and --port must be specified.

Note that if <conf> directory is specified, then it is always included first
in the classpath.
```

### 5. 테스트

```Plain
$ flume-ng agent --conf-file ./apache-flume-1.4.0-bin/conf/flume.conf --name agent
```

### 참고자료

[http://flume.apache.org/index.html](http://flume.apache.org/index.html)

[http://flume.apache.org/FlumeUserGuide.html](http://flume.apache.org/FlumeUserGuide.html)

[http://wawoops67.blogspot.kr/2013/05/flume-flume.html](http://wawoops67.blogspot.kr/2013/05/flume-flume.html)

[http://www.oss.kr/oss_repository6/85903](http://www.oss.kr/oss_repository6/85903)