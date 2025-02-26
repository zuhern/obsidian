---
tags:
  - Mysql
  - emma
Created: Invalid date
Updated: Invalid date
---
1. EMMA_unix_3_5_0.sh 실행

2. mysql 폴더 안의 ps 돌리기

3. ALTER TABLE em_smt_tran MODIFY column mt_pr int(11) NOT NULL auto_increment

4. 서버 올리기

cd /home/jsp/EMMA/

./emmasvc

- ** 이걸 실행 해야 초기에 테이블 생성됨

5. test query

insert into em_smt_tran (date_client_req, content, callback, service_type, broadcast_yn, msg_status, recipient_num) values(now(), 'Test Message 입니다', '07042845559', '0', 'N', '1', '01052499994');

6. 특수문자(이모티콘) 같은거 모바일에서 입력해도 에러나지 않는 인코딩

\#/etc/mysql/my.cnf

character-set-server = utf8mb4

collation-server = utf8mb4_unicode_ci

위와 같이 설정 되어 있으면 sms 발송 되지 않음

character-set-server = utf8

collation-server = utf8_unicode_ci