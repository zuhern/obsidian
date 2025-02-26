---
Created: Invalid date
Updated: Invalid date
---
moneymall-ceo

temp/LoadToTableAreaSales

camu에서 데이터를 가져와서

1시간 전 cart Direct와

n시간 전 every Click을 sessionsId로 조인

git pull

mvn -e -DskipTests clean install assembly:single -P hadoop-job -nsu

mvn -e -Dtest=LoadToTableAreaSalesTestSkip test -P prod -nsu

input

/moneymall/camus/destination/cart-view-direct-purchase-event/hourly

/moneymall/camus/destination/every-click-event/hourly

out

/moneymall/temp/areaSales