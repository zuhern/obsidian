---
Created: Invalid date
Updated: Invalid date
---
grand-for-site-day 소급하면 visitcnt만 값이 null로 나오고

그 후에

EventListToEveryClickEventTestDay 돌리기면 visitcnt도 채워진다.

master003에서 아래와 같이 빌드한 후

mvn -e -DskipTests clean install assembly:single -P hadoop-job -nsu

mvn -e -DconfPath=classpath*:/META-INF/spring/ceo-mr/*-test.xml,/META-INF/spring/spring-application-context-test.xml -DbeanName=eventListToEveryClickEventTestDayJobRunner -Dtest=CommonTestJobRunner test -P prod -nsu