---
Created: Invalid date
Updated: Invalid date
---
리눅스 포트열기iptables 이용하기!!$ iptables -A INPUT -p tcp --dport 8090 -j ACCEPT$ iptables -A OUTPUT -p tcp --dport 8090 -j ACCEPT포트번호ssh 22ftp 20,21web 80, 8080,443포트확인sudo iptables —list열린포트닫기$ iptables -D INPUT -s 69.36.233.0/24 -j DROP\# service iptables save // 저장하지 않으면... 재부팅하면 날라간다.. ㅡㅡ;;# service iptables restart