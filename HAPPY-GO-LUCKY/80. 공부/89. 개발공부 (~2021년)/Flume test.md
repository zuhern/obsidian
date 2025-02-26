---
Created: Invalid date
Updated: Invalid date
---
bin/flume-ng agent --conf-file /bigdata/apps/flume/conf/flume-conf.properties --name agent

bin/flume-ng agent --conf-file conf/single-node-demo.properties --name a1 --conf ./conf/ -Dflume.root.logger=INFO,console

bin/flume-ng agent --conf conf --conf-file example.conf --name a1 -Dflume.root.logger=INFO,console

**** 에러가 발생하면 맨 마지막줄을 잘 보자!!!!!!!!!!!!!!

[http://www.ashishpaliwal.com/blog/2013/12/flume-cookbook-quick-start/](http://www.ashishpaliwal.com/blog/2013/12/flume-cookbook-quick-start/)

노트 : 어떤 Flume의 속성들은 기본적으로 하드 디스크에 저장된다 초기에 기본으로 /tmp/flume 디렉토리가 사용된다 이것은 테스트하기에는 좋치만 실제 구동 환경에서는 flume.agent.logdir 속성에 저장하여 별도의 중복된 저장위치를 지정할 수 있다. 노트 : 만약 노드가 아래의 메시지를 뿌리고 꺼지거나 실행되길 거부할때에는 agent.FlumeNode: Aborting: Unexpected problem with environment.Failure to write in log directory: /tmp/flume. Check permissions? 그러면 /tmp/flume 디렉토리의 퍼미션을 조사해봐라. 오너나 유저가 속한 그룹으로 퍼미션을 추가해라  노트 :HDFS 파일이 정상적으로 끝날 때까지는 HDFS 파일이 지대로 써져있는지 보장이 없다. 이 때문에 콜렉터 싱크(Sink)는 주기적으로 파일을 닫고 새로운 파일을 연다. 파일 롤(파일을 닫고 여는 작업)의 시간은 30초이다. 만약 당신이 데이터를 2MB/s 보다 낮은 속도로 쓴다면 당신은 기본 시간을 늘려야 한다. 이는flume-site.xml 파일에서 flume.collector.roll.millis 와flume.agent.logdir.retransmit 를 설정하면 된다.