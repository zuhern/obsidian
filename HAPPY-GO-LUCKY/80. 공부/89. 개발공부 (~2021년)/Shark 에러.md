---
Created: Invalid date
Updated: Invalid date
---
/data01/shark/shark-0.9.1-bin-hadoop1/bin/shark -e "CREATE TABLE RESEARCH_every_click_item_view_tachyon AS SELECT * FROM every_click_item_view_tachyon”;

라고 날리면

Reloading cached RDDs from previous Shark sessions... (use -skipRddReload flag to skip reloading)

java.lang.IllegalAccessException: Class sun.reflect.misc.Trampoline can not access a member of class scala.None$ with modifiers "private"

Continuing ...

java.lang.RuntimeException: failed to evaluate: <unbound>=Class.new();

Continuing …

라고 에러가 나지만

Shark>

CREATE TABLE RESEARCH_every_click_item_view_tachyon AS SELECT * FROM every_click_item_view_tachyon;

는 됨.

Shark, Spark Kill

./spark-class org.apache.spark.deploy.Client kill spark://master002.prod.moneymall.ssgbi.com:7077 app-20140905110806-0047 (app번호)