---
Created: Invalid date
Updated: Invalid date
---
Hive는 데이터를 가지고 오면서

[/](http://hadoop002.prod.moneymall.ssgbi.com:50075/browseDirectory.jsp?dir=/&namenodeInfoPort=50070)[user](http://hadoop002.prod.moneymall.ssgbi.com:50075/browseDirectory.jsp?dir=/user&namenodeInfoPort=50070)/[hive](http://hadoop002.prod.moneymall.ssgbi.com:50075/browseDirectory.jsp?dir=/user/hive&namenodeInfoPort=50070)/[warehouse](http://hadoop002.prod.moneymall.ssgbi.com:50075/browseDirectory.jsp?dir=/user/hive/warehouse&namenodeInfoPort=50070)/ 밑에 하둡데이터를 move시키므로

Hive 안의 테이블을 지워도 데이터는 그대로 있어,

같은 이름의 테이블을 생성하면 이 전 데이터가 그대로 있으므로

이 경로 밑의 데이터를 지워주자.