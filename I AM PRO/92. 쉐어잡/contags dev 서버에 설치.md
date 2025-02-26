---
Created: Invalid date
Updated: Invalid date
---
http://khmirage.tistory.com/309

repogitory 설치하기

dev의 /srv/repo

git init

.git 폴더를 contags.server.git으로 변경

git config --bool core.bare true

source tree에서 repogitory 추가:: jsp@sharejob.iptime.org:/srv/repo/contags.server.git

~에 elastic 설치

wget [https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.4.0/elasticsearch-2.4.0.tar.gz](https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.4.0/elasticsearch-2.4.0.tar.gz)

wget [https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/2.4.0/elasticsearch-2.4.0.zip](https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/2.4.0/elasticsearch-2.4.0.zip)

ll

tar zxvf …

curl -XDELETE 'http://localhost:9200/firebase'

curl -X POST http://localhost:9200/firebase

screen -S contags

screen -R contags

screen -D -r contags

서비스 등록

scp ./scripts/hooks/post-receive jsp@sharejob.iptime.org:/srv/repo/introduce.server.git/hooks

scp ./scripts/hooks/post-receive manager@sharejob.me:/srv/repo/introduce.server.git/hooks

/etc/init/contags.server.conf 에 파일을 저장하면

sudo start contags.server 가 가능하다.

로그파일

[http://blueskai.tistory.com/101](http://blueskai.tistory.com/101)

crontab 이용

동작 순서를 살펴보면

1. cron.daily 에서 /usr/sbin/logrotate 호출

2. /usr/sbin/logrotate 에서 /etc/logrotate.conf 설정파일 참조

3. /etc/logrotate.conf 설정 파일에서 /etc/logrotate.d 참조 ( logrotate.conf 파일 안에 "include /etc/logrotate.d")

/etc/logrotate.d/ 밑에 파일 넣기

scp ./scripts/logrotate.d/introduce jsp@sharejob.iptime.org:/etc/logrotate.d

scp ./scripts/logrotate.d/introduce manager@sharejob.me:/etc/logrotate.d