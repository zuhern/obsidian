---
Created: Invalid date
Updated: Invalid date
---
— 수정

batch/src/main/resources/META-INF/sqoop/sqoop-import-amt-by-cornerid/lib/import.txt  
CornrSales  

— 서버

git pull

mvn -e -DskipTests clean install assembly:single -P prod -nsu

hadoop fs -ls lib

hadoop fs -rmr /user/moneymall/lib/moneymall-batch-0.5.0-RC10-SNAPSHOT-hadoop-job.jar

hadoop fs -put target/moneymall-batch-0.5.0-RC10-SNAPSHOT-hadoop-job.jar lib

hadoop fs -ls lib

— 로컬

mvn -e -DskipTests clean install assembly:single -P azkaban-daily -nsu