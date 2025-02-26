---
Created: Invalid date
Updated: Invalid date
---
오라클 11g 사용 도중 "비밀번호가 만료되었습니다." 라고 오류 발생

기본 비밀번호 만료 기간 설정 보기

SELECT RESOURCE_NAME, LIMIT FROM DBA_PROFILES WHERE PROFILE = 'DEFAULT';

RESOURCE_NAME                         LIMIT

- -----------------------------------------------------------------

......

PASSWORD_LIFE_TIME                     180

.....

PASSWORD_GRACE_TIME                   7

- -----------------------------------------------------------------

PASSWORD_LIFE_TIME 부분을 변경해야 한다.

ALTER PROFILE DEFAULT LIMIT PASSWORD_LIFE_TIME UNLIMITED;

프로파일이 변경되었습니다.

다음과 같이 확인한다.

SELECT USERNAME, ACCOUNT_STATUS, LOCK_DATE, EXPIRY_DATE FROM DBA_USERS WHERE USERNAME = 'USERNAME' ;

비밀번호가 만료된 유저는 다음과 같이 하여 비밀번호를 변경한다.

ALTER USER ACMSMW IDENTIFIED BY PASSWORD;

비밀번호 만료가 해제 됬는지 확인한다.

SELECT USERNAME, ACCOUNT_STATUS, LOCK_DATE, EXPIRY_DATE FROM DBA_USERS WHERE USERNAME = 'USERNAME' ;

**[출처]** [Oracle 잠금 계정 해제, 비밀번호 만료 해제](http://blog.naver.com/shavez/220491899457)|**작성자** [여포](http://blog.naver.com/shavez)