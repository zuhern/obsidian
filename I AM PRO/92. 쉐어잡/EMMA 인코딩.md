---
tags:
  - Mysql
  - emma
Created: Invalid date
Updated: Invalid date
---
특수문자(이모티콘) 같은거 모바일에서 입력해도 에러나지 않는 인코딩

\#/etc/mysql/my.cnf

character-set-server = utf8mb4

collation-server = utf8mb4_unicode_ci

위와 같이 설정 되어 있으면 sms 발송 되지 않음

character-set-server = utf8collation-server = utf8_unicode_ci