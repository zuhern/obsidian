---
Created: Invalid date
Updated: Invalid date
---
master003 에서 batch위치가서 git pull

1) mvn -e -DskipTests=true clean install [assembly:single](http://assemblysingle/) -P prod -nsu

2-1) mvn -e -Dtest=LoadToTableItemAroundClipForAnalyticsTestSkip test -P prod -nsu

2-2) mvn -e -DconfPath=/META-INF/spring/analytics/*-test.xml -DbeanName=analyticsDataToEveryClickItemViewEventJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu

hadoop fs -get 으로 꺼내거나 hadoop fs -getmerge로 합쳐서 꺼내거나

mvn -e -DconfPath=/META-INF/spring/analytics/*-test.xml -DbeanName=analyticsDataToEveryClickItemViewEventJobRunner -Dtest=GenericTestJobRunner test -P prod -nsu