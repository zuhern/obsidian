---
Created: Invalid date
Updated: Invalid date
---
sudo restart sharejob.me 가 잘 작동하면

ps -ef | grep share 했을 경우

/usr/bin/nodejs /srv/www/api.sharejob.me/bin/www

프로세스가 발생하나

갑자기 restart 명령어가 먹통인 상황에서

node /usr/bin/forever stop /srv/www/api.sharejob.me/bin/www

가 대신 있었다..