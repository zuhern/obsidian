---
Created: Invalid date
Updated: Invalid date
---
mysql -u root mysqlcd /etc/mysqltail -f /var/log/mysql/error.log***** 서버인 경우 cd /etc/mysql 수정bind-address 주석처리***** 사용자 등록CREATE DATABASE ‘share job’ /*!40100 DEFAULT CHARACTER SET utf8 COLLATE utf8_bin*/create user 'sharejob'@'%' identified by 'sharejob1234';grant all privileges on *.* to 'sharejob'@'%';grant all privileges on sharejob.* to 'sharejob'@'%';-- 로컬PC에서 mysql로 접속하기 위한 사용자 추가create user 'sharejob'@'localhost' identified by 'sharejob1234';-- 위 사용자에게 모든 것을 할 수 있는 권한 주기grant all privileges on *.* to 'sharejob'@'localhost';-- 위 사용자에게 특정 DB를 관리할 수 있는 권한 주기grant all privileges on sharejob.* to 'sharejob'@'localhost';