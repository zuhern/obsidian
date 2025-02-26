---
Created: Invalid date
Updated: Invalid date
---
mysql 서버 이전 으로 검색

* 본 블로그의 OS환경은 윈도우->리눅스 서버로 원격접속하여 모든 작업을 수행합니다.

* 덤프뜨는 방법은 여러가지 방법이 있겠지만

처음 하시는 분들이 가장 이해하기 쉬울거 같은(?) 방법으로 진행하겠습니다.

* 기존서버 A와 이전할 서버 B가있다는 가정아래 진행합니다.

* A서버와 B서버의 mysql버전은 4.1.21로 테스트된 내용입니다.

* 모든 경로는 절대경로로 작업하겠습니다.

* A서버와 B서버 모두 외부FTP(알FTP..등)접속이 가능한 서버이어야

본 블로그의 내용대로 작업하실 수 있습니다.

물론 다른 방법도 있습니다.

***-A서버 작업시작-***

가. Telnet 혹은 SSH로 A서버에 원격접속합니다. (원격접속방법은 본 블로그를 찾아보세요.)

나. A서버의 mysql설치경로 찾아가기

cd /usr/local/mysql/bin [엔터]

다. ls [엔터] mssqldump라는 파일(이놈이 dump의 핵심)이 있는지 확인.

라. /usr/local/mysql/bin/mysqldump -u root -p DB명 > 생성할 덤프파일명.sql [엔터]

마. 덤프뜰 A서버 SQL패스워드를 입력하고 [엔터] 잠시 대기..

바. A서버 덤프뜨기 완료.

사. ls [엔터] 생성한 덤프파일명.sql이 보이는지 확인.

아. 생성한 덤프파일을 A서버의 FTP홈디렉토리경로로 복사한다.

cp -r 생성한 덤프파일명.sql FTP홈디렉토리경로 [엔터]

참고로 보통의 경우 FTP홈디렉토리는 /home/FTP접속계정/으로 되어있다.

자. FTP홈디렉토리로 이동

cd /home/A서버 FTP접속계정 [엔터]

차. ls [엔터] 생성한 덤프파일이 정상적으로 복사되었는지 확인.

카. 알FTP를 실행하여 A서버 접속 후 생성한 덤프파일 내컴퓨터로 다운로드.

***-A서버 작업끝-***

***-B서버 작업시작-***

가. 알FTP실행하여 B서버 접속 후 다운로드 받은 덤프파일을 B서버에 업로드.

나. Telnet 혹은 SSH로 B서버에 원격접속합니다. (원격접속방법은 본 블로그를 찾아보세요.)

다. FTP홈디렉토리로 이동

cd /home/B서버 FTP접속계정 [엔터]

라. ls [엔터] 업로드한 덤프파일.sql이 보이는지 확인.

마. 업로드한 덤프파일을 B서버의 mysql설치경로로 이동한다.

cp -r 업로드한 덤프파일.sql /usr/local/mysql/bin [엔터]

아. mysql 설치경로를 찾아가기

cd /usr/local/mysql/bin [엔터]

자. ls [엔터] 파일복사가 제대로 됬는지 확인.

차. 덤프 밀어넣기

 /usr/local/mysql/bin/mysql -u root -p 밀어넣을 B서버DB명 < 업로드한 덤프파일명.sql [엔터]

카. 밀어넣을 B서버 SQL패스워드를 입력하고 [엔터] 잠시 대기..

타. 덤프 밀어넣기 완료.

***-B서버 작업끝-***

**-*기타 참고정보-***

1. 덤프뜨기  
mysqldump -u 사용자계정 -p 데이터베이스명 테이블명 > 저장될 파일명  
예) mysqldump -u root -p mydb_name > mydb_name.sql  
이렇게 하면 mydb_name을 모두 덤프를 뜨게된다.  
테이블만 덤프를 뜨고 싶다면  
예) mysqldump -u root -p mydb_name member > mydb_name.member.sql  
이렇게 하면 원하는 테이블만 덤프를 뜰 수 있다.  
2. 복구하기  
mysql -u 사용자계정 -p DB명 < 덤프파일명  
예) mysql -u root -p < 덤프파일명.sql  
예) mysql -u root -p mydb_name < 덤프파일명.테이블명.sql  

1.특정 db의 특정 table에서 원하는 값만 덤프받기  
>> edu라는 디비에 a,b,c라는 테이블이 있다.  

여기서 a라는 테이블에서 no가 7번이상이고 10번  
이하인 값만 덤프를 받고자 한다. 어떻게 하겠는가?  
여기서 사용되는 옵션은 -w 이다.그럼 위 질문의 sql문은 아래와 같다  

mysqldump -u mysql_admin -p edu a -w'no=>7 and no=<10' > edu_a_cond.sql  
위와같이 하면 no가 7~10번까지가 덤프될것이다.  
위에서 조건문은 -w 다음에 싱글쿼테이션으로 묶어준다.  

sql에서 사용하는 조건문이 다 될듯싶다.

모두 테스트를 해보진 않았다.  
2.디비 스키마(Schema)만 백업받기  
>>초기에 작성해 놓은 테이블 스키마가 없을때 어떻게 하겠는가?  
만약 하나의 테이블이라면 desc 해서 일일이 다 삽질을 하면 되것지만  

만약 테이블이 100개라면 ..크억...이럴때 사용하는 mysqldump옵션이 있습니다.  
-d 입니다.  
!.edu라는 디비의 모든 테이블 스키마를 백업받으려면  
mysqldump -u mysql_admin -p -d edu > edu_db.sql  
!.edu라는 디비의 a라는 테이블 스키마를 백업받으려면  
mysqldump -u mysql_admin -p -d edu a> edu_a_table.sql  

[Option Information]

--opt  
[--quick --add-locks --add-drop-table --extended-insert]  
원복을 할때 기존 DB와 TABLE, DATA를 삭제하고 백업한 내용으로 Update를 합니다.  

-q, --quick  
버퍼를 사용하지 않고 바로 표준출력으로 보낸다.  

--add-locks  
테이블의 덤프하기전에 해당 테이블을 잠그고 덤프한 후에 테이블을 풀어준다.  

--add-drop-table  
덤프 결과에서 create table 앞에 drop table 절을 추가한다.  

-c, --complte-insert  
INSERT 구문에서 필드명을 포함한 전체를 덤프  

--extended-insert  
INSERT문 하나에서 모든 레코드를 삽입하는 INSERT문을 생성합니다.  

-f, --force  
덤프 중 에러가 있어도 계속 진행  

-h, --host  
특정 호스트의 MySQL 에서 데이터 덤프  

-t, --no-create-info  
테이블 생성 정보는 덤프하지 않음(데이터만 덤프)  

-d, --no-data  
테이블 스키마만 덤프  

--default-character-set=euckr character set 지정

--extended-insert=FALSE 분리된 query문으로 작성

원문 : [http://blog.daum.net/webdevil/4181036](http://blog.daum.net/webdevil/4181036)