---
Created: Invalid date
Updated: Invalid date
---
trulia : 직방같은 회사

2억명 정도의 잠재고객에게 맞는 recommendation을 제공

3%로씩 양쪽중개인에게 중개비를 지불

고객의 성향에 맞는 서비스를 제공하는 것이 중요하다

ex) 메일을 아침에 받는 것을 좋아하는 고객, 메일보다 DM을 좋아하는 고객... 등

2백만불짜리 팔면 6만불 받음 (초봉정도)

relevant Content & Relevant UX 제공

1. High quality content : 사이트의 컨텐츠 : 같은 집인데 다른 집인 것처럼 나올 수 있다.

2. High quality user tracking

3. High quality modeling

4. In timely manner

고객이 어떤 것을 검색하는지 그중에서 어떤것을 선택하는지 파악

- > 모델링을 잘해서 데이터에서 고객의 기호를 추출해내는 것이 중요하다.
- > 고객의 행동을 계산을 실시간으로 해낼 수 있어야한다. real time <- 한 사이트를 방문하고 다시 오는 경우가 적기 때문에

데이터 양, 데이터 처리 속도 등의 이유로 빅데이터를 이용한다.

사용자가 스스로 찾아낼 수 있을 정보를 미리 제공함으로서 고객이 쉽게 원하는 정보를 갖을 수 있도록 한다.

개인정보.. 트랙킹할 때 개인정보가 들어가지 않은 데이터를 추출하는 것으로 가능하면 노력하고

개인정보가 필요하면 암호화 등의 처리를 한다.

data warehouse : 가비지 데이터가 들어오지 않도록 컨트롤

data science

data pipeline :  make it scale, real time processing

product development : 50~60 milions / a month, 3 bilion events / a month

pieces them together to contribute to "traffic"

---

hadoop

HDFS : data node , name node

server spec : 64 ~ 128기가 메모리 정도, 총

a distributed system for counting words.

map : key & value

suffle : group by

reduce : sum

Yarn

---

Cassandra

HBase의 데이터 모델을 가져다 씀

큰 차이는 분배처리에서 어떻게 처리를 하는가

HBase는 master slave

카산드라는 P2P

personalization

고객들의 검색하는 것을 알고 그것으로 더 좋은 것을 고객에게 주는

고객은 시간이 많지가 않아

고객에게 접근한다 고객에게

테슬라에서 일했을 때

광고는 waste야

나랑 관계없으면

고객이 원하는 중요하는 데이터를 갖고 (풋프린트)

kafka : 버퍼..

zookeeper

---

state를 캡처하지 말고 fact를 캡쳐하라

fact : 저장했다 지웠다. 액션하나하나

state : 현재 저장한 것이 몇개냐

fact로 state를 뽑아낼 수 있다.

scala 로 cascading 로 맵리듀스 코딩

---

실시간 이벤트는 사용하지 않는 곳이 거의 없을 정도

real real time으로

일배치 보다 실시간으로 알려준다.