---
Created: Invalid date
Updated: Invalid date
---
brew install tomcat

/usr/local/Cellar/tomcat/8.5.11 에 설치됨

$ sudo vi /usr/local/Cellar/tomcat/8.5.11/libexec/conf/server.xml

<Host name="localhost"  appBase="webapps"

이 부분을

<Host name="localhost"  appBase="/Users/color106/webapps"으로 바꿔주면 된다.