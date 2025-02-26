---
Created: Invalid date
Updated: Invalid date
---
VirtualBox에 Linut / Red Hat (64bit) minimum으로 설치

1.네트워크 설정

VirtualBox에서 네트워크 호스트전용 (내PC와연결), NAT (인터넷) 을 추가 *****호스트가 NAT보다 앞번호여야함

VirtualBox에 리눅스 설치하기 전에 윗줄을 먼저 하면 eth1이 자동으로 추가되어 있다.

- ifcfg-eth0 수정

vi /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0

HWADDR=08:00:27:B9:CC:01

TYPE=Ethernet

ONBOOT=yes

NM_CONTROLLED=yes

BOOTPROTO=static

IPADDR=192.168.56.99

GATEWAY=192.168.56.1

NETMASK=255.255.255.0

- ifcfg-eth1 수정

vi /etc/sysconfig/network-scripts/ifcfg-eth1

DEVICE=eth1

HWADDR=08:00:27:65:71:44

TYPE=Ethernet

UUID=334a5f08-06d9-438d-9995-721d93904902

ONBOOT=yes

NM_CONTROLLED=yes

BOOTPROTO=dhcp

ifconfig 로 확인

2. update

yum update

3. scp 설치

yum install openssh-clients

4. 웹상에서 Java, Maven 다운받고 /opt/ 에 압축풀기

wget http://download.oracle.com/otn-pub/java/jdk/7u51-b13/jdk-7u51-linux-x64.tar.gz

scp jdk-7u51-linux-x64.tar.gz 192.168.56.99:./

mv 압축파일 /opt

tar zxvf 압축파일

rm 압축파일

ln -s 압축푼폴더 jdk

5. Git 설치

yum install git

6.환경변수

vi /etc/profile

export JAVA_HOME=/opt/jdk

export MAVEN_HOME=/opt/maven

export PATH=$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin

#\#export PATH=/usr/local/bin:/bin:/usr/bin:/user/local/sbin:/usr/sbin:/sbin:$JAVA_HOME/bin:$MAVEN_HOME/bin

7.확인

env

java -version

mvn —version

git -version