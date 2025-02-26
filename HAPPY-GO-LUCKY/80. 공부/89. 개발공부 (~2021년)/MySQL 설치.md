---
Created: Invalid date
Updated: Invalid date
---
- mac 설치

brew install homebrew/versions/mysql55

mysql_sequre_installation

mysql 설치 후 다음과 같이 password 재설정

$>mysql -uroot -p

mysql -u sharejob -p

mysql >show databases;

ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.

mysql >SET PASSWORD = PASSWORD('new_password');

데이터베이스 만들기

mysql >create database share job;

사용자 생성

CREATE USER 'sharejob'@`'192.168.0.%'` IDENTIFIED BY 'sharejob1234';

GRANT ALL PRIVILEGES ON *.* TO 'sharejob'@`'192.168.0.%';`

SHOW GRANTS FOR 'sharejob'@`'192.168.0.%';`

FLUSH privileges;

CREATE USER 'sharejob'@'localhost' IDENTIFIED BY 'sharejob1234';

GRANT ALL PRIVILEGES ON *.* TO 'sharejob'@'localhost';

SHOW GRANTS FOR 'sharejob'@'localhost';

FLUSH privileges;

테이블 생성 (sql file 사용)

- 리눅스 mysql 설치

sudo apt-get install mysql-server-5.5 mysql-client-5.5

mysql서버 외부에서 붙도록 하는 설정

cd etc/mysql/my.cnf

bind-address 주석처리

`sudo apt-get update` `sudo apt-get upgrade`

sudo apt-get install mysql-server-5.6 `--fix-missing --fix-broken`

alter session set current_schema=scott;