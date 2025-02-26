---
Created: Invalid date
Updated: Invalid date
---
* 화면

management-report

* 화면 경로

/moneymall/moneymall-src/management/management-reporter/src/main/resources/web/tabAll.html

* 설명

하둡 시스템 쪽

맵, 하둡잡, 리얼타임, 백업 잘 돌았나. 모니터링 하는 화면

* 서버 올리기 kafka001

server : wrapper

/data01/moneymall-apps/management-report/

web : tomcat

10.203.5.28/data01/tomcat/apache-tomcat-7.0.50/webapps/ROOT/web

* 내부 화면

/moneymall/moneymall-src/management/management-reporter/src/main/resources/web/distributionReport.html

* 특징 :

Daily랑 RealTime은 NetezzaDao를 사용하고, Hdfs 는 HdfsBackupDao, HBase는 HBaseBackupDao를 사용

ehCache를 사용한다. 한시간 마다 갱신이 되고 Dao로 조회할 때 ehCache에 key로 검색하여 데이터가 있으면 그 데이터를 사용하고

없으면 DB에 조회한 후 데이터를 ehCache에도 key, value로 저장한다.