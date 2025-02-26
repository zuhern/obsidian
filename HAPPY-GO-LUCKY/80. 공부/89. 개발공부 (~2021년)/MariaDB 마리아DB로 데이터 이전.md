---
Created: Invalid date
Updated: Invalid date
---
서버 maridDB에서 로컬 mariaDB로 데이터 이전

===============================================================================

서버 ===============================================================================

sql 파일로 덤프 뜨기 (~에서 함)

mysqldump -u root -p CEO_REPORT > CEO_REPORT.sql

FTP로 서버로 sql 파일을 로컬로 다운로드

===============================================================================

로컬 ===============================================================================

sql 파일을 마리아DB bin 위치로 이동 (꼭 이동해야하는지는 모르겠으나 Downloads 폴더에서는 안됨)

cp CEO_REPORT.sql /usr/local/Cellar/mariadb/5.5.36/bin/

데이터를 넣을 databases 생성

create batabase CEO_REPORT

/usr/local/Cellar/mariadb/5.5.36/bin/ 위치에서 밑의 명령어 호출

mysql -u root -p CEO_REPORT < CEO_REPORT.sql