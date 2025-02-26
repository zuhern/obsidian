---
Created: Invalid date
Updated: Invalid date
---
ls -al

halt -h now 종료

scp jdk-7u51-linux-x64.tar.gz moneymall@192.168.56.99:./

scp 소스파일 복사할위치(192.168.56.99:./) secure copy protocol

ssh 192.168.56.99 cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized-keys

ssh 소스서버 cat 소스파일 >> 타겟파일 - 다른 서버에 있는 정보를 이 서버로 가지고 온다.

ping 네트워크 동작 확인 (-c : 보낼 패킷 수 지정)

ifconfig 네트워크 정보 (하단에 IP있음)

/etc/init.d/network restart 네트워크 전체 다시 시작

wget 다운로드 받기

rm -rf 파일삭제 (옵션:확인없이)

ln -s 링크 (버전이 변경되면 압축을 푼 폴더명도 바뀌므로 jdk같이 링크를 걸어서 쓴다)

mv 이동

tar -zxvf 압축풀기 (-z:gzip으로 압축,해제

-x:압축된 파일을 압축해제

-v:처리중인 파일을 자세하게 보여주기

-f, —file [HOSTNAME:]F 저장파일 혹은 장치파일 F에 저장

tar -cvzf 압축하기 (tar cvzf hadoop.tar.gz hadoop)

rm 삭제

env 현재의 환경을 보여준다

cat 파일 내용 j보기

iptables -F 방화벽

## 현재 떠 있는 프로세서 ##

ps -ef | grep mysql

ps -ef | grep

ps -ef

jps -l

리눅스 라인 카운트

cat every_click_item_view_20140916.txt | wc -l