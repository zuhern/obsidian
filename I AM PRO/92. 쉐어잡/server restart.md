---
tags:
  - Mysql
  - Server
  - Sharejob
Created: Invalid date
Updated: Invalid date
---
ssh jsp@192.168.0.108

(0414)  
DEBUG=app* npm start  

**** mysql**

sudo service mysql status  
sudo service mysql startsudo service mysql stop  

tail -f /var/log/mysql/error.log  
sudo netstat -an | grep 3306  

sudo /etc/init.d/mysql restart

**** api**

sudo restart sharejob.me

**** SMS**

./emmasvc start

**** 서버 rollback**

git --work-tree=/srv/www/api.sharejob.me --git-dir=/srv/repo/api.sharejob.me.git checkout <hash or tagname>

git --work-tree=/srv/www/api.sharejob.me --git-dir=/srv/repo/api.sharejob.me.git log --graph

git --work-tree=/srv/www/api.sharejob.me --git-dir=/srv/repo/api.sharejob.me.git checkout b46b028

**** 파일복사**

scp ./post-receive manager@sharejob.me:/srv/repo/web.sharejob.me.git/hooks

**** git push**

git push dev

git push azure

**설정 변경**

/srv/www/api.sharejob.me/scripts/sharejob.me.conf