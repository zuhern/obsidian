---
Created: Invalid date
Updated: Invalid date
---
index 생성 및 삭제

curl -XDELETE http://localhost:9200/firebase

curl -X POST http://localhost:9200/firebase

`{ "index" : { "analysis" : { "tokenizer" : { "comma" : { "type" : "pattern", "pattern" : "," } }, "analyzer" : { "comma" : { "type" : "custom", "tokenizer" : "comma" } } } } }`

curl -XGET 'http://localhost:9200/firebase/_search?q=contact.phoneNumber:*9669*'

curl -XGET 'http://localhost:9200/firebase/user/_search' -d '{"query": {"term": {"email":"zuhern"}}}'

curl -XGET 'http://localhost:9200/firebase/user/_search' -d '{"query": {"term": {"tags.tag":"apple"}}}'

[[]]

1. main테이블에 값의 변화가 있으면 elastic의 지정 index에 변동값을 저장한다.

2. 화면에서 검색을 하면 search/request에 검색 조건을 저장한다. 그리고 search/response의 값이 변동되기를 기다린다.

3. search/request 값변동이 있으면 elastic에서 쿼리한 후 결과 값을 search/response에 넣는다.

- field name 검색하기

[https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-field-names-field.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping-field-names-field.html)

`PUT phrase/doc/1 { "text": "St Peter Fm some other text Cape Basin" } GET phrase/_search { "query": { "bool": { "must": [ {"match_phrase": {"text": "St Peter Fm"}}, {"match_phrase": {"text": "Cape Basin"}} ] } } }`