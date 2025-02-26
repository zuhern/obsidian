---
Created: Invalid date
Updated: Invalid date
---
start-all.sh

한 후에

[bigdata@server01 ~]$ hadoop fs -mkdir /input

으로 폴더 생성한 후

[bigdata@server01 ~]$ hadoop fs -copyFromLocal hadoop/*.txt /input

txt 파일을 input에 넣고

[bigdata@server01 ~]$ hadoop fs -ls /input

파일들이 복사가 되었는지 확인