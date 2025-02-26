---
tags:
  - Hive
Created: Invalid date
Updated: Invalid date
---
select * from every1 where mbrid=‘0000079241';

0000079241 3 11 43 30

select * from base1 where mbrid=‘0000079241';

0000079241 3 11 43 30(excel확인)

---

select * from order1 where mbrid='0000079241’;

0000079241 2 5

select * from orderflat1 where mbrid='0000079241’;

0000079241 20140407282563 1000005014392

0000079241 20140407282563 0000005585435

0000079241 20140407282563 0000003148896

0000079241 20140407283002 0000004455030

0000079241 20140407283002 0000004275709

---

select * from search1 where mbrid='0000079241’;

0000079241 39 13

select * from searchflat1 where mbrid=‘0000079241';

0000079241 39 13(excel확인)

---

select * from cart1 where mbrid='0000079241’;

0000079241 12 12

select * from cartflat1 where mbrid='0000079241’;

0000079241 1038985068

0000079241 1038988646

0000079241 1038994006

0000079241 1038994412

0000079241 1038584805

0000079241 1038973678

0000079241 1038583457

0000079241 1038583959

0000079241 1038580669

0000079241 1038582451

0000079241 1038581398

0000079241 1038582229

---

select * from item1 where mbrid='20658346';

20658346 5 3

select * from itemflat1 where mbrid='20658346';

20658346 0000005688230

20658346 1000005329972

20658346 1000005330900

20658346 1000005330900

20658346 1000005329972

---

select * from allDate where mbrid='0000079241';

0000079241 2014-04 3 2 5 12 12 0 0 11 43 30 39 13

select

e.mbrid

,e.pcidcnt

,o.ordcnt

,o.orditemcnt

,c.cartcnt

,c.cartitemcnt

,i.clipcnt

,i.clipitemcnt

,e.mypagecnt

,e.viewcnt

,e.viewitemcnt

,s.srchcnt

,s.srchitemcnt

from every1 e

Left Outer Join order1 o on e.mbrid = o.mbrid  
Left Outer Join search1 s on e.mbrid = s.mbrid  

Left Outer Join cart1 c on e.mbrid = c.mbrid  
Left Outer Join item1 i on e.mbrid = i.mbrid  

WHERE e.mbrid='0000079241’;

0000079241 3 2 5 12 12 NULL NULL 11 43 30 39 13

---

mvn -e -Dtest=AnalyticsIf2_4ItemAroundFlatTestSkip test -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_4ItemAroundTestSkip test -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_4OrderEventFlatTestSkip test -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_4OrderEventTestSkip test -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_4SearchKeywordFlatTestSkip test -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_4SearchKeywordTestSkip test -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_4EveryClickEventTestSkip test -P prod -nsu

mvn -e -Dtest=AnalyticsIf2_4EveryClickEventFlatTestSkip test -P prod -nsu

/moneymall/analytics/if2-1/analytics-if-2-1-every-click-event

/moneymall/analytics/if2-1/analytics-if-2-1-order-event

/moneymall/analytics/if2-1/analytics-if-2-1-search-keyword

/moneymall/analytics/if2-1/analytics-if-2-1-cart-view

/moneymall/analytics/if2-1/analytics-if-2-1-item-around

/moneymall/analytics/if2-1/analytics-if-2-1

CREATE EXTERNAL TABLE base1(

mbrid STRING

,pcid STRING

,itemid STRING

,pageviewtype STRING

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-every-click-event-union/2014-04/';

CREATE EXTERNAL TABLE every1(

mbrid STRING

,pcidcnt BIGINT

,mypagecnt BIGINT

,viewcnt BIGINT

,viewitemcnt BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-every-click-event/2014-04/';

CREATE EXTERNAL TABLE order1(

mbrid STRING

,ordcnt BIGINT

,orditemcnt BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-order-event/2014-04/';

CREATE EXTERNAL TABLE orderflat1(

mbrid STRING

,orderno STRING  
,itemid STRING  

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-order-event-flat/2014-04/';

CREATE EXTERNAL TABLE search1(

mbrid STRING

,srchcnt BIGINT

,srchitemcnt BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-search-keyword/2014-04/';

CREATE EXTERNAL TABLE searchflat1(

mbrid STRING

,srchWd STRING

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-search-keyword-flat/2014-04/';

CREATE EXTERNAL TABLE cart1(

mbrid STRING

,cartcnt BIGINT

,cartitemcnt BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-cart-view/2014-04/';

CREATE EXTERNAL TABLE cartflat1(

mbrid STRING

,itemid STRING

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-cart-view-flat/2014-04/';

CREATE EXTERNAL TABLE item1(

mbrid STRING

,clipcnt BIGINT

,clipitemcnt BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-item-around/2014-04/';

CREATE EXTERNAL TABLE itemflat1(

mbrid STRING

,itemid STRING

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1-item-around-flat/2014-04/';

CREATE EXTERNAL TABLE allDate(

mbrid STRING

,date STRING

,pcidcnt BIGINT

,ordcnt BIGINT

,orditemcnt BIGINT

,cartcnt BIGINT

,cartitemcnt BIGINT

,clipcnt BIGINT

,clipitemcnt BIGINT

,mypagecnt BIGINT

,viewcnt BIGINT

,viewitemcnt BIGINT

,srchcnt BIGINT

,srchitemcnt BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-1/analytics-if-2-1/2014-04/';