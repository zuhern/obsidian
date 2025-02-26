---
Created: Invalid date
Updated: Invalid date
---
[http://wiki.moneymall.ssgadm.com:8010/pages/viewpage.action?pageId=2916521&src=contextnavpagetreemode](http://wiki.moneymall.ssgadm.com:8010/pages/viewpage.action?pageId=2916521&src=contextnavpagetreemode)

애널리틱스5 shell, sql name.sh, name.sql

1. proc_clear

2. proc_clear2 # 잘 모르겠음…

3. proc_input_ord

4. proc_input_clck # every click은 하둡에서 가져오는 걸로, item 가지고 오는 부분은 모르겠다. 테이블 정보를 모른다.

5. proc_std_ctg_conf

6. proc_shopp_std_ctg_conf

7. proc_mbr_std_ctg_index_ord # temp_mbr_std_ctg_index_ord_mbr 에 last_id, mm 이 꼭 필요한건지는 모르겠음.. 일단 지운다.. 바로 밑 click처럼 해도 될것같은데 왜 delete insert로 하는 걸까요?

8. proc_mbr_std_ctg_index_clck

9. proc_brand_conf

10. proc_mbr_brand_index_ord \# temp_mbr_std_ctg_index_ord_mbr 또 사용

11. proc_mbr_brand_index_clck

12. proc_temp_table_drop

13. proc_mbr_std_ctg_score

14. proc_mbr_brand_score # 8번처럼 해도 될것같은데 왜 drop create insert로 하는 걸까요?

15. proc_temp_table_drop2

16. proc_mbr_shopp_score

17. proc_mbr_shopp_score_potential

18. proc_temp_table_drop3

rm -rf *.sh

rm -rf sql/*  
rm -rf sqoop/*  

scp *.sh moneymall@10.203.5.32:/data01/research-shell/

scp sql/*.sql moneymall@10.203.5.32:/data01/research-shell/sql

scp sqoop/*.txt moneymall@10.203.5.32:/data01/research-shell/sqoop

analytics5_01_proc_clear.job

analytics5_02_proc_clear2.job

analytics5_03_proc_input_ord.job

analytics5_04_java_input_clck.job

analytics5_04_proc_input_clck.job

analytics5_05_proc_std_ctg_conf.job

analytics5_06_proc_shopp_std_ctg_conf.job

analytics5_07_proc_mbr_std_ctg_index_ord.job

analytics5_08_proc_mbr_std_ctg_index_clck.job

analytics5_09_proc_brand_conf.job

analytics5_10_proc_mbr_brand_index_ord.job

analytics5_11_proc_mbr_brand_index_clck.job

analytics5_12_proc_temp_table_drop.job

analytics5_13_proc_mbr_std_ctg_score.job

analytics5_14_proc_mbr_brand_score.job

analytics5_15_proc_temp_table_drop2.job

analytics5_16_proc_mbr_shopp_score.job

analytics5_17_proc_mbr_shopp_score_potential.job

analytics5_18_proc_temp_table_drop3.job

everyclick : /user/hive/warehouse/research.db/research_every_click_event_view

mvn -e -Dtest=AnalyticsIf5_04EveryClickEventTestSkip test -P prod -nsu

jCascalog vs Hive Test

mvn -e -Dtest=AnalyticsIf5_17MbrShoppScorePotentialTestSkip test -P prod -nsu

jdbc:mysql://10.203.9.205:3306/DW -> jdbc:sqlserver://10.203.9.21:17001/SCOM_ODS

proc_clear.sh

proc_clear2.sh

proc_input_ord.sh

proc_input_clck.sh

proc_std_ctg_conf.sh

proc_shopp_std_ctg_conf.sh

proc_mbr_std_ctg_index_ord.sh

proc_mbr_std_ctg_index_clck.sh

proc_brand_conf.sh

proc_mbr_brand_index_ord.sh

proc_mbr_brand_index_clck.sh

proc_temp_table_drop.sh

proc_mbr_std_ctg_score.sh

proc_mbr_brand_score.sh

proc_temp_table_drop2.sh

proc_mbr_shopp_score.sh

proc_mbr_shopp_score_potential.sh

proc_temp_table_drop3.sh