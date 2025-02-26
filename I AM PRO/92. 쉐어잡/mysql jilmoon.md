---
Created: Invalid date
Updated: Invalid date
---
CREATE USER 'jilmoon'@'%' IDENTIFIED BY 'sharejob1234';GRANT ALL PRIVILEGES ON jilmoon.* TO 'jilmoon'@'%';SHOW GRANTS FOR 'jilmoon'@'%';FLUSH privileges;CREATE USER 'jilmoon'@'192.168.0.%' IDENTIFIED BY 'sharejob1234';GRANT ALL PRIVILEGES ON jilmoon.* TO 'jilmoon'@'192.168.0.%';SHOW GRANTS FOR 'jilmoon'@'192.168.0.%';FLUSH privileges;CREATE USER 'jilmoon'@'localhost' IDENTIFIED BY 'sharejob1234';GRANT ALL PRIVILEGES ON jilmoon.* TO 'jilmoon'@'localhost';SHOW GRANTS FOR 'jilmoon'@'localhost';FLUSH privileges;