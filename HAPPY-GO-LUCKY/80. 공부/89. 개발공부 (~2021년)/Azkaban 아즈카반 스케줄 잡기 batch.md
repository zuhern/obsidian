---
Created: Invalid date
Updated: Invalid date
---
1. 소스 수정

2. 로컬 코멘드 창에서

mvn -e -DskipTests clean install assembly:single -P azkaban-daily -nsumvn -e -DskipTests clean install assembly:single -P azkaban-all -nsu

mvn -e -DskipTests clean install assembly:single -P azkaban-job-ceo -nsu

3. target 폴더에 zip 파일 생성됨

4. azkaban page에 들어가서 해당 스케줄 삭제 -> 프로젝트 삭제

5. 프로젝트 생성한 후 (삭제한 프로젝트와 같은 명이면 미리 복사) upload로 3번에서 말한 zip파일을 올림

6. 서버에 src 위치에 가서 git pull 상단, 하단 둘 다 install (하단 assembly)

7.

mvn -e -DskipTests clean install assembly:single -P prod -nsu

mvn -e -DskipTests clean install assembly:single -P hadoop-job -nsu

batch/target 에 jar 새성됨

8.

hadoop fs -ls /user/moneymall/lib/

hadoop fs -rmr /user/moneymall/lib/moneymall-batch-0.5.0-RC10-SNAPSHOT-hadoop-job.jar

hadoop fs -put target/moneymall-batch-0.5.0-RC10-SNAPSHOT-hadoop-job.jar lib

hadoop fs -ls /user/moneymall/lib/

9. 스케줄 : 9시간 전으로 UTC

데일리 : 01시

mvn -e -DskipTests clean install assembly:single -P azkaban-ten-minutes -nsu  
mvn -e -DskipTests clean install assembly:single -P azkaban-store-capacity-info -nsu  

Back up 에서 도는 것들 (ten minute)

hadoop fs -D fs.default.name=hdfs://master001-backup.

[prod.moneymall.ssgbi.com:9000](http://prod.moneymall.ssgbi.com:9000/)

-rmr /user/moneymall/lib/moneymall-batch-0.5.0-RC9-SNAPSHOT-hadoop-job.jar

hadoop fs -D fs.default.name=hdfs://master001-backup.[prod.moneymall.ssgbi.com:9000](http://prod.moneymall.ssgbi.com:9000/) -put target/moneymall-batch-0.5.0-RC9-SNAPSHOT-hadoop-job.jar lib

hadoop fs -D fs.default.name=hdfs://master001-backup.[prod.moneymall.ssgbi.com:9000](http://prod.moneymall.ssgbi.com:9000/) -ls lib