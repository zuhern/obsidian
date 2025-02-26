---
Created: Invalid date
Updated: Invalid date
---
클래스 검색 : http://wiki.moneymall.ssgadm.com:8010/pages/viewpage.action?pageId=1836635&src=search

데이터 없음

1)

select substr(CRITN_DT,5,4),CRITN_DT from (select distinct CRITN_DT from IF_BIGDATA_PZREGION_RESPONSE where CRITN_DT = now()-1) a;

lt-table-campaign-response

ERROR - input path [/moneymall/event/campaign-event/2014-08-03] does not exist!

2)

select substr(CRITN_DT,5,4),CRITN_DT from (select distinct CRITN_DT from IF_BIGDATA_CLICKEVENT_RAW_DATA where CRITN_DT = now()-1) a;

lt-table-item-around-event.job

ERROR - input path [/moneymall/event/item-around-event/2014-08-03] does not exist!