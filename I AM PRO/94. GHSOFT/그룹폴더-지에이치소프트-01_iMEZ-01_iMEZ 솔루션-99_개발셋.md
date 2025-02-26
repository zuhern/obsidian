---
Created: Invalid date
Updated: Invalid date
URL: https://drive.worksmobile.com/#WORKS=true&MSGN=ACTION_GET_SHARE_LIST_111&MSGV=MTg0NTY4MHwzNDcyMzU0Nzg4Nzc3MjYwMjkyfDM0NzIzNTkzNzU1NTM5Mjg5NjV8LzAxX2lNRVovMDFfaU1FWiDshpTro6jshZgvOTlf6rCc67Cc7IWLL2h0dHBkL3xAMTg0NTY4MHx8VQ--&PAGEV=1
---
그룹폴더/지에이치소프트/01_iMEZ/01_iMEZ 솔루션/99_개발셋

1.

프로젝트 포트 바꾸고

경로를 / 로 바꾸고

server.xml 을 복사하여

Servers 하위인 tomcat 의 server.xml 로 엎어치기

2.

File > import > general > preferences

gms_ide_preference.epf 파일 선택해서 import 하시고 finish

3.

window > preferences > java > code style > fommatter

4.

httpd-2.2.25-win32-x86-openssl-0.9.8y.msi 설치

5.

그룹폴더/지에이치소프트/01_iMEZ/01_iMEZ 솔루션/99_개발셋/httpd

C:\IDE\servers\httpd2.2.25 폴더 밑에 conf 폴더, module 폴더 엎어치기

apache 설치후 실행 중인 경우에는 module 폴더 엎어치기 안되니 끄고 하기

-Denv="local"