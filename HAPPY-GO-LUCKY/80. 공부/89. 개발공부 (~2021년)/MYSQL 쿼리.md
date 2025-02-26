---
Created: Invalid date
Updated: Invalid date
---
1. string으로 받은 todate를 date로 바꾼 후 어제날짜를 받고 그 날짜를 다시 String으로 바꾼다

DATE_FORMAT(DATE_ADD(STR_TO_DATE(\#TODATE#, '%y/%m/%d'),INTERVAL 1 DAY),'%Y%m%d’)

DATE_FORMAT(DATE_ADD(STR_TO_DATE(NOW(), '%y/%m/%d'),INTERVAL 1 DAY),'%Y%m%d’)

DATE_FORMAT(DATE_ADD(NOW(),INTERVAL -30 DAY),'%Y%m%d')