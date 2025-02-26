---
Created: Invalid date
Updated: Invalid date
---
1. * 화면 경로
2. /moneymall/moneymall-src/management/management-reporter/src/main/resources/web/dashboard/monitor.html

* 관련 링크

[SSG-BigData Home](http://wiki.moneymall.ssgadm.com:8010/display/bigdata/SSG-BigData+Home) / [System Constitution](http://wiki.moneymall.ssgadm.com:8010/display/bigdata/System+Constitution) / [Moneymall Monitoring](http://wiki.moneymall.ssgadm.com:8010/display/bigdata/Moneymall+Monitoring)

Ganglia: [http://master002.prod.moneymall.ssgbi.com/ganglia/](http://master002.prod.moneymall.ssgbi.com/ganglia/)

Graphite: [http://master001.prod.moneymall.ssgbi.com/](http://master001.prod.moneymall.ssgbi.com/)

설명 : 시스템 리소스들.. 모든 서버들이 정상 작동하는지 모니터링 함

* Graphite

우측 Dashboard ->

tab의 첫번째 버튼 Dashboard -> Find -> 종류 선택 -> 좌측트리에서 추가할 그래프 선택

tab의 첫번째 버튼 Dashboard -> Edit Dashboard : title이랑 alias 수정 (target : 데이터 선들)

tab의 첫번째 버튼 Dashboard -> Save As : 저장

그래프 클릭 -> Graph Operations -> Direct URL

* Ganglia

그래프 클릭 클릭 URL 복사

Graphite 모니터링 화면 경로 : 10.203.9.198(Dev) ,/data01/jenkins/apache-tomcat-7.0.42/webapps/ROOT

———> web 만 바꿔주면 됨