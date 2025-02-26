---
tags:
  - Azkaban
Created: Invalid date
Updated: Invalid date
---
analytics-if-2-1-every-click-event

analytics-if-2-1-order-event

analytics-if-2-1-search-keyword

analytics-if-2-1-cart-view

analytics-if-2-1-item-around

analytics-if-2-1

analyticsIf2_1EveryClickEventBaseUnionJobRunner

analyticsIf2_1EveryClickEventBaseJobRunner

analyticsIf2_1EveryClickEventJobRunner

analyticsIf2_1OrderEventJobRunner

analyticsIf2_1SearchKeywordJobRunner

analyticsIf2_1CartViewJobRunner

analyticsIf2_1ItemAroundJobRunner

analyticsIf2_1JoinJobRunner

- pom.xml 수정함

azkaban-analytics -> azkaban-analytics-1

azkaban-analytics-2 생성

azkaban-analytics.xml -> azkaban-analytics-1.xml

azkaban-analytics-2.xml 생성

/azkaban/analytics/ -> /azkaban/analytics-1/

/azkaban/analytics-2/ 생성

mvn -e -DskipTest clean install assembly:single -P azkaban-analytics-1 -nsu

mvn -e -DskipTest clean install assembly:single -P azkaban-analytics-2 -nsu