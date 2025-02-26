---
Created: Invalid date
Updated: Invalid date
---
—-로그인

mysql -u root -p

—-계정생성 및 비밀번호 설정 (로컬접속계정)

create user 'willbe'@'localhost' identified by 'will be’;

—-권한설정

grant all privileges on *.* to 'willbe'@'localhost' with grant option;

—-계정생성 및 비밀번호 설정 (외부접속계정)

Create user 'willbe'@'%' identified by ‘will be’;

—-권한설정

grant all privileges on *.* to 'willbe'@'%' with grant option;