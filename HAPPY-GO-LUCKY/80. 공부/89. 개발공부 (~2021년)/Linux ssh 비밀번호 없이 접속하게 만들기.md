---
Created: Invalid date
Updated: Invalid date
---
1. 각각의 서버에서 id_rsa.pub 생성 (hosts, network 에서 HOSTNAME 수정 후)

ssh-keygen -t rsa

rm -rf .ssh;ssh-keygen -t rsa;

2. 한 서버에 authorized_keys 파일을 생성하고 모든 각각의 서버의 id_rsa.pub 에 있는 정보를 모은다.

cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

chmod 755 authorized_keys

ssh 192.168.56.98 cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

ssh server03 cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

3. authorized_keys 파일을 각각의 다른 서버에 복사한다.

scp ~/.ssh/authorized_keys server02:~/.ssh/authorized_keys authorized_keys

scp ~/.ssh/authorized_keys 192.168.56.97:~/.ssh/authorized_keys

4. ssh server01; ssh 192.167.56.99 로 접속하였을 때 비밀번호를 묻지 않으면 성공