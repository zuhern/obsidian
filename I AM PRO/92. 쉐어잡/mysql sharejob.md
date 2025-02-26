---
tags:
  - Mysql
  - Server
  - Sharejob
Created: Invalid date
Updated: Invalid date
---
live  
mysql -u root -p mysql  
password: @share  
// 계정 추가  
// root 계정으로 로그인  
CREATE USER 'sharejob'@'%' IDENTIFIED BY 'sharejob1234';  
GRANT ALL PRIVILEGES ON *.* TO 'sharejob'@'%';  
SHOW GRANTS FOR 'sharejob'@'%';  
FLUSH privileges;  
CREATE USER 'sharejob'@'192.168.0.%' IDENTIFIED BY 'sharejob1234';  
GRANT ALL PRIVILEGES ON *.* TO 'sharejob'@'192.168.0.%';  
SHOW GRANTS FOR 'sharejob'@'192.168.0.%';  
FLUSH privileges;  
CREATE USER 'sharejob'@'localhost' IDENTIFIED BY 'sharejob1234';  
GRANT ALL PRIVILEGES ON *.* TO 'sharejob'@'localhost';  
SHOW GRANTS FOR 'sharejob'@'localhost';  
FLUSH privileges;  
select user, host from user;