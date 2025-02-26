---
Created: Invalid date
Updated: Invalid date
---
커밋 한다음에

cd /data01/moneymall-src/service/service-ceo/

kafka002 (10.203.5.27) 에서 git pull 한 후

빌드하고

`mvn -e -DskipTests=``**true**` `clean install assembly:single -P prod -nsu`

서버실행

mvn -e -Dtest=CeoHttpServerTestSkip test -P prod -nsu