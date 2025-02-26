---
Created: Invalid date
Updated: Invalid date
---
```Plain
exp meta_ddl/willbe123$@IMETA_189 FILE='c://data1/platon/0808008' GRANTS=Y INDEXES=Y ROWS=N CONSTRAINTS=Y TRIGGERS=Y COMPRESS=Y DIRECT=N CONSISTENT=N STATISTICS=ESTIMATE OWNER=META_DDL


1)export명령
- 무조건하기
exp 사용자ID/암호@오라클인스턴스명 file=백업할 파일명 indexes=yes grants=yes constraints=yes

- 테이블 골라서 하기
exp 사용자ID/암호@오라클인스턴스명 file=백업할 파일명 indexes=yes grants=yes constraints=yes
tables=category,cat_template,template

2)improt 명령
- 무조건하기
imp 오라클사용자명/암호@인스턴스명 file=덤프파일이름 fromuser=익스포트한사용자ID touser=임포트할ID

- 스키마 스크립트 추출하기
imp 오라클사용자명/암호@인스턴스명 file=덤프파일이름 fromuser=익스포트한사용자ID touser=임포트할ID
indexfile=스크립트명

- 이미 테이블있으면 무시하고 작업하기
imp 오라클사용자명/암호@인스턴스명 file=덤프파일이름 fromuser=익스포트한사용자ID touser=임포트할ID
ignore=yes


3)user 생성하기
- Tablespace생성
CREATE TABLESPACE wfmdata
DATAFILE
' 경로 ' SIZE 2048 M    (예:   'e:\oracle\abc.dbf' )
LOGGING
DEFAULT NOCOMPRESS
ONLINE
PERMANENT
EXTENT MANAGEMENT LOCAL AUTOALLOCATE

- 유저생성
Create user 유저명 identified by 패스워드;
grant dba to 유저명
```

- default tablespace지정

ALTER USER 유저명 DEFAULT TABLESPACE HC_WFMDATA;