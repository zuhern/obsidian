---
Created: Invalid date
Updated: Invalid date
---
# 검증 방법

소스이벤트를 flatten만 한 데이터와

가공한 데이터를 각각 Hive로 Select하여 비교하였다.

---

# **결과 데이터 위치**

-every-click-event

/moneymall/analytics/if2-4/analytics-if-2-4-every-click-event

/moneymall/analytics/if2-4/analytics-if-2-4-order-event

/moneymall/analytics/if2-4/analytics-if-2-4-search-keyword

/moneymall/analytics/if2-4/analytics-if-2-4-cart-view

/moneymall/analytics/if2-4/analytics-if-2-4-item-around

**검증 데이터 위치**/moneymall/analytics/if2-4/analytics-if-2-4-every-click-event-flat

/moneymall/analytics/if2-4/analytics-if-2-4-order-event-flat

/moneymall/analytics/if2-4/analytics-if-2-4-search-keyword-flat

/moneymall/analytics/if2-4/analytics-if-2-4-cart-view-flat

/moneymall/analytics/if2-4/analytics-if-2-4-item-around-flat

---

# **테스트 명령어**

mvn -e -Dtest=AnalyticsIf2_4ItemAroundFlatTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4ItemAroundTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4OrderEventFlatTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4OrderEventTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4SearchKeywordFlatTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4SearchKeywordTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4EveryClickEventTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4EveryClickEventFlatTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4CartViewTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4CartViewFlatTestSkip test -P prod -nsu  
mvn -e -Dtest=AnalyticsIf2_4JoinTestSkip test -P prod -nsu  

---

# EVENT 전체 테이블을 아우터 조인한 결과 데이터 검증

select  
e.mbrid  
,e.pcidcnt  
,o.ordcnt  
,o.orditemcnt  
,c.cartcnt  
,c.cartitemcnt  
,c.cartlist  
,i.clipcnt  
,i.clipitemcnt  
,i.cliplist  
,e.mypagecnt  
,e.viewcnt  
,e.viewitemcnt  
,s.srchcnt  
,s.srchitemcnt  
from every4 e  
Left Outer Join order4 o on e.mbrid = o.mbrid  
Left Outer Join search4 s on e.mbrid = s.mbrid  
Left Outer Join cart4 c on e.mbrid = c.mbrid  
Left Outer Join item4 i on e.mbrid = i.mbrid  
WHERE e.mbrid='0000013354';  

WHERE e.mbrid='0000001788';  
0000001788 1 NULL NULL 32 32 1067427605|1067398240|1067422283 NULL NULL NULL 0 17 16 64 45  
select * from all4 WHERE mbrid='0000001788';  
0000001788 2014-06-08 1 0 0 32 32 1067427605|1067398240|1067422283 0 0 0 17 16 64 45  

WHERE e.mbrid='0000013354';  
0000013354 2 1 8 17 17 1067481839|1067529150|1067472088 NULL NULL NULL 2 31 28 4 4  
select * from all4 WHERE mbrid='0000013354';  
0000013354 2014-06-08 2 1 8 17 17 1067481839|1067529150|1067472088 0 0 2 31 28 4 4  

---

# **EVERY CLICK EVENT 검증**

select * from every4 where mbrid='20907204';

"!mbr-id", "!pc-id-cnt", "!!my-page-cnt", "!!view-cnt", "!!view-item-cnt"  
20907204 1 3 2 1  

select * from everyflat4 where mbrid='20907204';

20907204 13978891737789384851816 MY_PAGE  
20907204 13978891737789384851816 MY_PAGE  
20907204 13978891737789384851816 1000005558368 ITEM_VIEW_PAGE  
20907204 13978891737789384851816 1000005558368 ITEM_VIEW_PAGE  
20907204 13978891737789384851816 MY_PAGE  

---

# CART VIEW 검증

select * from cart4 where cartcnt !=cartitemcnt;

"!mbr-id", "!cart-cnt", "!cart-item-cnt", "!cart-item-3max"(**장바구니 담은 아이템 이름(최대3개)**)

0002223580 8 7 1067538583|1067539102|1067536418

select * from cartflat4 where mbrid = '0002223580';

0002223580 1067536418  
0002223580 1067537482  
0002223580 1067538121  
0002223580 1067538583  
0002223580 1067538825  
0002223580 1067534794  
0002223580 1067539102  
0002223580 1067539102  

---

# **ITEM AROUND EVENT 검증**

select * from item4 where clipcnt !=clipitemcnt;

"!mbr-id", "!clip-cnt", "!clip-item-cnt", "!item-list"(**클립에 담은 아이템 이름 (최대3개)**)

20586992 10 9 0000007696673|0000007690576|0000006613866

select * from itemflat4 where mbrid = '20586992';

20586992 0000008976246  
20586992 0000008055922  
20586992 0000008976246  
20586992 0000006613866  
20586992 0000008060350  
20586992 0000007690576  
20586992 0000007696673  
20586992 1000004876013  
20586992 0000006615109  
20586992 0000007095585  

---

# **SEARCH KEYWORD 검증**

select * from search4 where mbrid='20907160';

"!mbr-id", "!srch-cnt", "!srch-item-cnt"

20907160 12 4

select * from searchflat4 where mbrid='20907160';  
20907160 유기농설탕  
20907160 유기농설탕  
20907160 유기농설탕  
20907160 유기농설탕  
20907160 소금  
20907160 오늘의반가  
20907160 유기농설탕  
20907160 유기농설탕  
20907160 유기농설탕  
20907160 유기농설탕  
20907160 소금  
20907160 걸이  

---

# **ORDER EVENT 검증**

select * from order4 where mbrid='20906467';

"!mbr-id", "!ord-cnt", "!ord-item-cnt"

20906467 3 4

select * from orderflat4 where mbrid='20906467';  
20906467 20140608699276 1000005564101  
20906467 20140608699276 1000005267862  
20906467 20140608699910 1000005267920  
20906467 20140608702121 1000005551459  

---

# **HIVE 테이블생성 쿼리**

CREATE EXTERNAL TABLE every4(  
mbrid STRINGc ttfcffvvedd  
,pcidcnt BIGINT  
,mypagecnt BIGINT  
,viewcnt BIGINT  
,viewitemcnt BIGINT  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-every-click-event/2014-06-08/';  

CREATE EXTERNAL TABLE everyflat4(  
mbrid STRING  
,pcid STRING  
,itemid STRING  
,pageviewtype STRING  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-every-click-event-flat/2014-06-08/';  

CREATE EXTERNAL TABLE order4(

mbrid STRING  
,ordcnt BIGINT  
,orditemcnt BIGINT  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-order-event/2014-06-08/';  

CREATE EXTERNAL TABLE orderflat4(  
mbrid STRING  
,orderno STRING  
,itemid STRING  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-order-event-flat/2014-06-08/';  

CREATE EXTERNAL TABLE search4(  
mbrid STRING  
,srchcnt BIGINT  
,srchitemcnt BIGINT  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-search-keyword/2014-06-08/';  

CREATE EXTERNAL TABLE searchflat4(  
mbrid STRING  
,srchWd STRING  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-search-keyword-flat/2014-06-08/';  

CREATE EXTERNAL TABLE cart4(  
mbrid STRING  
,cartcnt BIGINT  
,cartitemcnt BIGINT  
,cartlist STRING  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-cart-view/2014-06-08/';  

CREATE EXTERNAL TABLE cartflat4(  
mbrid STRING  
,itemid STRING  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-cart-view-flat/2014-06-08/';  

CREATE EXTERNAL TABLE item4(  
mbrid STRING  
,clipcnt BIGINT  
,clipitemcnt BIGINT  
,cliplist STRING  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-item-around/2014-06-08/';  

CREATE EXTERNAL TABLE itemflat4(  
mbrid STRING  
,itemid STRING  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4-item-around-flat/2014-06-08/';  

CREATE EXTERNAL TABLE all4(  
mbrid STRING  
,date STRING  
,pcidcnt BIGINT  
,ordcnt BIGINT  
,orditemcnt BIGINT  
,cartcnt BIGINT  
,cartitemcnt BIGINT  
,cartlist STRING  
,clipcnt BIGINT  
,clipitemcnt BIGINT  
,cliplist STRING  
,mypagecnt BIGINT  
,viewcnt BIGINT  
,viewitemcnt BIGINT  
,srchcnt BIGINT  
,srchitemcnt BIGINT  
) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'  
LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if2-4/analytics-if-2-4/2014-06-08/';