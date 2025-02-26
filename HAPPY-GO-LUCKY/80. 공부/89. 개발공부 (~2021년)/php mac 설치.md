---
Created: Invalid date
Updated: Invalid date
---
[http://jason.pureconcepts.net/2014/11/install-apache-php-mysql-mac-os-x-yosemite/](http://jason.pureconcepts.net/2014/11/install-apache-php-mysql-mac-os-x-yosemite/)

1. 설치하기

`sudo su -`

`apachectl start`http:localhost

2. httpd.conf 셋팅 바꾸기

`cd /etc/apache2/ cp httpd.conf httpd.conf.bak`

`sudo vi /etc/apache2/httpd.conf`

`LoadModule deflate_module libexec/apache2/mod_deflate.so` `LoadModule expires_module libexec/apache2/mod_expires.so` `LoadModule rewrite_module libexec/apache2/mod_rewrite.so`

`LoadModule php5_module libexec/apache2/libphp5.so`

<IfModule dir_module>

DirectoryIndex index.html index.php

</IfModule>

3. 확인하기

`grep DocumentRoot httpd.conf`

4. 재시동

sudo apachectl start

5. 소스 위치

The default `DocumentRoot` for Mac OS X Yosemite is `/Library/WebServer/Documents`