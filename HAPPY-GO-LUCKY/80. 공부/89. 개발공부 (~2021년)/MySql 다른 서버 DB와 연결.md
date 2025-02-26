---
Created: Invalid date
Updated: Invalid date
---
SQL Server 다른 서버에 있는 DB와 연결하기▦이리 2014.07.24 10:46

DB를 사용하다 보면 다른 서버에 있는 DB 내용이 필요할 때가 있다.

SSMS를 2개 열어놓고 사용해도 되긴 하지만(..) 바로 SELECT 해와서 INSERT같은 작업을 할때 더 편하게 작업을 하려면 서버를 링크해서 작업하면 작업이 한결 수월해진다.

출처 : http://ndolson.com/229

먼저 서버를 링크 합니다.

EXEC sp_addlinkedserver

@server='real_server',  -- 앞으로 사용할 링크드 서버이름입니다.

@srvproduct = '', -- 공백처리 합니다.

@provider = 'SQLOLEDB', -- SQL 서버이면 그대로 씁니다.

@datasrc = 'AAA.BBB.CCC.DDD', -- 아이피 적어 줍니다.

@provstr='',   -- 공백처리 합니다.

@catalog='DB'   -- 특정 카다로그 즉 데이터 베이스 이름을 적습니다.

GO

다음 서버 로그인을 만듭니다.

EXEC sp_addlinkedsrvlogin 'real_server', 'false', NULL, 'id', 'password'

현재 로그인한 서버와 연결하고자 하는 서버 id, password가 동일하면 위 작업은 생략해도 됩니다.

연결 후에는 아래와 같이 쿼리를 실행합니다.

SELECT * FROM real_server.DB.소유자.테이블