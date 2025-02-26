---
Created: Invalid date
Updated: Invalid date
---
hive -e -> /data01/shark/shark-0.9.2/bin/shark -e

hive -f -> /data01/shark/shark-0.9.2/bin/shark -i

타키온 : 테이블명_tachyon

/data01/shark/shark-0.9.2/bin/shark -e "SELECT site_name, shopp_id, std_ctg_depth_id, sum(weight) as weight FROM(SELECT t1.site_name, t1.shopp_id, t2.given_ctg as std_ctg_depth_id, t2.confidence as weight FROM RESEARCH.shopp_std_ctg_depth t1 LEFT OUTER JOIN RESEARCH.tb_ord_std_ctg_conf t2 ON t1.std_ctg_depth_id=t2.to_ctg ) t3 WHERE std_ctg_depth_id IS NOT NULL GROUP BY site_name, shopp_id, std_ctg_depth_id"

Time taken: 8.643 seconds

hive -e "SELECT site_name, shopp_id, std_ctg_depth_id, sum(weight) as weight FROM(SELECT t1.site_name, t1.shopp_id, t2.given_ctg as std_ctg_depth_id, t2.confidence as weight FROM RESEARCH.shopp_std_ctg_depth t1 LEFT OUTER JOIN RESEARCH.tb_ord_std_ctg_conf t2 ON t1.std_ctg_depth_id=t2.to_ctg ) t3 WHERE std_ctg_depth_id IS NOT NULL GROUP BY site_name, shopp_id, std_ctg_depth_id”

Time taken: 35.077 seconds, Fetched: 27103 row(s)

—— 전체 테스트 ——

1. hive

2. shark tachyon

—— job 1개로 테스트 ——

1. jCascalog

mvn -e -Dtest=AnalyticsIf5_17MbrShoppScorePotentialTestSkip test -P prod -nsu

17m 34s

1,054.551 sec

2. hive

analytics5_17_proc_mbr_shopp_score_potential.job

5m 6s

317s

3. shark

기존 hive 테이블 이용해서 명령어를 날린다.

11m 10s

4. shark tachyon

m s

5. hive tachyon

m s

279s

* shark로 만든 테이블에 hive로 쿼리를 날리니 에러가 난다.

[proc_clear.sh](http://proc_clear.sh/)

[proc_clear2.sh](http://proc_clear2.sh/)

[proc_input_ord.sh](http://proc_input_ord.sh/)

[proc_input_clck.sh](http://proc_input_clck.sh/)

[proc_std_ctg_conf.sh](http://proc_std_ctg_conf.sh/)

[proc_shopp_std_ctg_conf.sh](http://proc_shopp_std_ctg_conf.sh/)

[proc_mbr_std_ctg_index_ord.sh](http://proc_mbr_std_ctg_index_ord.sh/)

[proc_mbr_std_ctg_index_clck.sh](http://proc_mbr_std_ctg_index_clck.sh/)

[proc_brand_conf.sh](http://proc_brand_conf.sh/)

[proc_mbr_brand_index_ord.sh](http://proc_mbr_brand_index_ord.sh/)

[proc_mbr_brand_index_clck.sh](http://proc_mbr_brand_index_clck.sh/)

[proc_temp_table_drop.sh](http://proc_temp_table_drop.sh/)

[proc_mbr_std_ctg_score.sh](http://proc_mbr_std_ctg_score.sh/)

[proc_mbr_brand_score.sh](http://proc_mbr_brand_score.sh/)

[proc_temp_table_drop2.sh](http://proc_temp_table_drop2.sh/)

[proc_mbr_shopp_score.sh](http://proc_mbr_shopp_score.sh/)

[proc_mbr_shopp_score_potential.sh](http://proc_mbr_shopp_score_potential.sh/)

[proc_temp_table_drop3.sh](http://proc_temp_table_drop3.sh/)