---
Created: Invalid date
Updated: Invalid date
---
kafka002

cd /data01/moneymall-src/service/service-ceo/

git pull

mvn -e -DskipTests clean install assembly:single -P tomcat-war -nsu

cd /data01/tomcat/apache-tomcat-7.0.52

bin/shutdown.sh

cd webapps/

rm -rf ROOT ROOT.war

cp /data01/moneymall-src/service/service-ceo/target/ROOT.war .

cd ../

bin/startup.sh

locahost

cd /Users/zuhern/moneymall/moneymall-src/service/service-ceo/

mvn -e -DskipTests clean install assembly:single -P tomcat-war -nsu

cd /bigdata/apps/tomcat/

bin/shutdown.sh

cd webapps/

rm -rf ROOT ROOT.war

cp /Users/zuhern/moneymall/moneymall-src/service/service-ceo/target/ROOT.war .

cd ../

bin/startup.sh

로컬

rm -rf /bigdata/apps/tomcat/webapps/ROOT/view/resultOfCornerSales.html

cp ~/moneymall/moneymall-src/service/service-ceo/src/main/resources/web/view/resultOfCornerSales.html /bigdata/apps/tomcat/webapps/ROOT/view/

서버

rm -rf /data01/tomcat/webapps/ROOT/view/resultOfCornerSales.html

cp /data01/moneymall-src/service/service-ceo/src/main/resources/web/view/resultOfCornerSales.html /data01/tomcat/apache-tomcat-7.0.52/webapps/ROOT/view/