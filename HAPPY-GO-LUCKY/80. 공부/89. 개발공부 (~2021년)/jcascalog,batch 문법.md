---
Created: Invalid date
Updated: Invalid date
---
**1.**

Distinct 랑 Count는 한번에 할 수 없다.

**2.** Join은 한번에 한번씩만

**3.** CascalogFunction 상속받은 함수는 Mapper

CascalogAggregator 상속받은 함수는 Reducer 이다.

**4.** Count는 로우를 카운트함

**5.** Subquery distinctPcidQuery = new Subquery("!site-no","!ckwhere","!pcid")

.predicate(baseQuery, "!site-no","!ckwhere","!pcid","_")  
.predicate(Option.DISTINCT, true);  

4번째 컬럼을 뺀다는 의미

List

inputTap = generateEvent();// 여기서 필요한 EveryClick만 Flatten한다.  
Subquery baseQuery = new Subquery("!disp-ctg-id","!cornr-id","!pc-id","!mbr-id")  
.predicate(inputTap, "!disp-ctg-id","!cornr-id","!pc-id","!mbr-id");  
Subquery finalQuery = new Subquery("!disp-ctg-id","!cornr-id","!mbr-id")  
.predicate(baseQuery, "!disp-ctg-id","!cornr-id","_","!mbr-id");  
Api.execute(new StdoutTap(), finalQuery);