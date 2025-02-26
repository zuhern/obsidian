---
Created: Invalid date
Updated: Invalid date
---
## Wrapper

## **Request Handler 배포**

- Request Handler 서버는 Vert.X 서버로 두대의 서버에서 동작하고 있다.

- Server : 202.8.173.148 / 202.8.173.149

- 배포 작업은 동시에 하면 안되고 서버 하나씩 순차적으로 진행해야 함.

---------------------------

Deploy Command

---------------------------

ssh 202.8.173.148

user : scom

pwd : 새우깡!@#

## Build & Packaging

——————————————————

cd /data01/request-handler/

git pull

mvn -e -DskipTests clean install [assembly:single](http://assemblysingle/) -P prod -nsu

## Server stop  
——————————————————  

cd /data01/moneymall-apps/request-handler/

./bin/runner stop

## 기존 Binary 삭제

——————————————————

rm -rf /data01/moneymall-apps/request-handler/

mkdir /data01/moneymall-apps/request-handler/

cd /data01/request-handler/target/

cp request-handler-0.1.0-SNAPSHOT-stand-alone.zip /data01/moneymall-apps/request-handler/

(cp ./target/request-<version>-stand-alone.zip /data01/moneymall-apps/request-handler/)

## 서버 구동  
——————————————————  

cd /data01/moneymall-apps/request-handler/

unzip request-handler-0.1.0-SNAPSHOT-stand-alone.zip

\chmod a+x -R bin

./bin/runner start &

## 확인

——————————————————

cd /data02/logs/moneymall

tail -f collection-logger.log