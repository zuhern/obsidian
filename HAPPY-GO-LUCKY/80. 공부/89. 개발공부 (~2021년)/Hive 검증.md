---
Created: Invalid date
Updated: Invalid date
---
CREATE EXTERNAL TABLE cart(

mbrid STRING

,itemid STRING

,increase BIGINT

,decrease BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if/analytics-if-cart-item-quantity-change-event/';

CREATE EXTERNAL TABLE item(

mbrid STRING

,itemid STRING

,viewpagecount BIGINT

,scrollrangesum BIGINT

,scrollrangemax BIGINT

,staytermsum BIGINT

,lastvisitconvert TIMESTAMP

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if/analytics-if-item-view-event/';

CREATE EXTERNAL TABLE order(

mbrid STRING

,itemid STRING

,count BIGINT

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if/analytics-if-order-view-event/';

select c.mbrid, c.itemid, o.count, c.increase, c.decrease

, i.viewpagecount, i.scrollrangesum, i.scrollrangemax, i.staytermsum, i.lastvisitconvert

from cart c

inner Join item i on c.mbrid = i.mbrid and c.itemid = i.itemid

inner Join order o on c.mbrid = o.mbrid and c.itemid = o.itemid

where c.mbrid = '20791969';

20791969 0000002209734 1 0 1 1 1 70453 2014-05-20 22:29:39.725 1

20791969 0000005432944 1 0 1 0 0 20655 2014-05-20 22:21:18.832 1

20791969 0000008610119 1 0 1 5 5 24641 2014-05-20 22:25:57.239 1

20791969 0000008694345 1 0 1 2 2 31829 2014-05-20 22:24:21.308 1

CREATE EXTERNAL TABLE analy(

mbrid STRING

,itemid STRING

,count BIGINT

,increase BIGINT

,decrease BIGINT

,viewpagecount BIGINT

,scrollrangesum BIGINT

,scrollrangemax BIGINT

,staytermsum BIGINT

,lastvisitconvert TIMESTAMP

) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'

LINES TERMINATED BY '\n' STORED AS TEXTFILE LOCATION '/moneymall/analytics/if/analytics-data-interface/';

select * from analy where mbrid = '20791969';

20791969 0000002209734 1 1 0 1 1 1 70453 2014-05-20 22:29:39.725

20791969 0000005432944 1 1 0 1 0 0 20655 2014-05-20 22:21:18.832

20791969 0000008610119 1 1 0 1 5 5 24641 2014-05-20 22:25:57.239

20791969 0000008694345 1 1 0 1 2 2 31829 2014-05-20 22:24:21.308